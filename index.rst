:allow_comments: False

.. _`Godot Docs – *master* branch`:

Tài liệu Godot – nhánh *master*
===============================

.. only:: not i18n

  .. note:: Tài liệu Godot có sẵn bằng nhiều ngôn ngữ và phiên bản khác nhau. Mở rộng bảng "Read the Docs" ở cuối thanh bên để xem danh sách.

.. only:: i18n

  .. note:: Tài liệu này được các thành viên cộng đồng dịch từ `bản tiếng Anh gốc <https://docs.godotengine.org/en/stable>`_ trên `Weblate <https://hosted.weblate.org/projects/godot-engine/godot-docs>`_.

            Tùy vào mức độ hoàn tất của quá trình dịch, bạn có thể thấy những đoạn văn hoặc toàn bộ trang vẫn còn bằng tiếng Anh. Bạn có thể hỗ trợ cộng đồng bằng cách cung cấp bản dịch mới hoặc đánh giá các bản dịch hiện có trên Weblate.

            Hiện tại, bản dịch bản địa hóa chỉ có sẵn cho nhánh "stable". Bạn vẫn có thể xem tài liệu tiếng Anh cho các phiên bản engine khác bằng bảng "Read the Docs" ở cuối thanh bên.

Chào mừng bạn đến với tài liệu chính thức của `Godot Engine <https://godotengine.org>`__, engine game 2D và 3D miễn phí, mã nguồn mở, do cộng đồng phát triển! Nếu bạn mới làm quen với tài liệu này, chúng tôi khuyên bạn nên đọc
:ref:`trang giới thiệu <doc_about_intro>` để có cái nhìn tổng quan về những nội dung mà tài liệu này cung cấp.

Để bắt đầu đọc tài liệu phù hợp, hãy chọn ô tương ứng với hồ sơ của bạn:

.. raw:: html

    <style>
        .grid-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr;
            gap: 0.375rem;
            grid-auto-flow: row;
            grid-template-areas:
            "new-to-game know-game-learn-godot"
            "know-godot-learn-godot contribute-to-godot";
        }

        .grid-item {
            padding: 1rem;
            border-radius: 0.375rem;
            text-align: center;
        }

        .grid-item,
        .grid-item:visited {
            color: hsla(0, 0%, 100%, 0.9);
        }

        .grid-item:hover,
        .grid-item:focus {
            text-decoration: none;
            filter: brightness(120%);
        }

        .grid-item:active {
            filter: brightness(80%);
        }

        .new-to-game {
            grid-area: new-to-game;
            background-color: #166534;
        }

        .know-game-learn-godot {
            grid-area: know-game-learn-godot;
            background-color: #115e59;
        }

        .know-godot-learn-godot {
            grid-area: know-godot-learn-godot;
            background-color: #1e3a8a;
        }

        .contribute-to-godot {
            grid-area: contribute-to-godot;
            background-color: #831843;
        }
    </style>
    <div class="grid-container">
        <a class="grid-item new-to-game" href="about/introduction.html">
            Tôi chưa từng làm game,<br>
            <strong>Tôi muốn làm một game.</strong>
        </a>
        <a class="grid-item know-game-learn-godot" href="getting_started/step_by_step/index.html">
            Tôi biết cách làm game,<br>
            <strong>Tôi muốn biết cách sử dụng Godot.</strong>
            </a>
        <a class="grid-item know-godot-learn-godot" href="tutorials/index.html">
            Tôi biết cách sử dụng Godot,<br>
            <strong>Tôi muốn tìm hiểu thêm về các chủ đề nâng cao của Godot.</strong>
        </a>
        <a class="grid-item contribute-to-godot" href="https://contributing.godotengine.org/en/latest/index.html">
            Tôi biết cách sử dụng Godot,<br>
            <strong>Tôi muốn đóng góp cho Godot.</strong>
        </a>
    </div>
    <br>

Bạn cũng có thể sử dụng mục lục trong thanh bên để dễ dàng truy cập bất kỳ phần nào của tài liệu về chủ đề mình quan tâm. Bạn cũng có thể sử dụng chức năng tìm kiếm ở góc trên bên trái.

.. _`Get involved`:

Tham gia đóng góp
-----------------

Godot Engine là một dự án mã nguồn mở do cộng đồng tình nguyện viên phát triển. Nhóm tài liệu luôn cần phản hồi và sự hỗ trợ của bạn để cải thiện các hướng dẫn và tài liệu tham chiếu lớp. Nếu bạn không hiểu điều gì đó hoặc không thể tìm thấy nội dung mình cần trong tài liệu, hãy giúp chúng tôi cải thiện tài liệu bằng cách cho chúng tôi biết!

Hãy gửi issue hoặc pull request trên `repository GitHub <https://github.com/godotengine/godot-docs/issues>`_, giúp chúng tôi `dịch tài liệu <https://hosted.weblate.org/engage/godot-engine/>`_ sang ngôn ngữ của bạn, hoặc trò chuyện với chúng tôi trên ``#documentation`` channel trong `Godot Contributors Chat <https://chat.godotengine.org/>`_!

.. centered:: |weblate_widget|

.. _`Offline documentation`:

Tài liệu ngoại tuyến
--------------------

Để xem tài liệu ngoại tuyến, bạn có thể tải xuống bản HTML (được cập nhật vào mỗi thứ Hai): `stable <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-stable.zip>`__, `latest <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-master.zip>`__, `3.6 <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-3.6.zip>`__. Giải nén kho lưu trữ ZIP rồi mở ``index.html`` cấp cao nhất trong trình duyệt web.

Đối với thiết bị di động hoặc máy đọc sách điện tử, bạn cũng có thể tải xuống bản ePub (được cập nhật vào mỗi thứ Hai): `stable <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-stable.zip>`__, `latest <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-master.zip>`__, `3.6 <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-3.6.zip>`__. Giải nén kho lưu trữ ZIP rồi mở tệp ``GodotEngine.epub`` trong ứng dụng đọc sách điện tử.

.. Below is the main table-of-content tree of the documentation website.
   It is hidden on the page itself, but it makes up the sidebar for navigation.

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Giới thiệu
   :name: sec-general

   about/introduction
   about/list_of_features
   about/system_requirements
   about/faq
   about/complying_with_licenses
   about/release_policy
   about/docs_changelog

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Bắt đầu
   :name: sec-learn

   getting_started/introduction/index
   getting_started/step_by_step/index
   getting_started/first_2d_game/index
   getting_started/first_3d_game/index


.. Sections below are split into two groups. First come meta sections, covering
   general matters. Below that different areas of the engine are listed.
   These sections are sorted alphabetically. Please keep them that way.
.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Hướng dẫn sử dụng
   :name: sec-tutorials

   tutorials/best_practices/index
   tutorials/troubleshooting
   tutorials/editor/index
   tutorials/migrating/index

   tutorials/2d/index
   tutorials/3d/index
   tutorials/animation/index
   tutorials/assets_pipeline/index
   tutorials/audio/index
   tutorials/export/index
   tutorials/io/index
   tutorials/i18n/index
   tutorials/inputs/index
   tutorials/math/index
   tutorials/navigation/index
   tutorials/networking/index
   tutorials/performance/index
   tutorials/physics/index
   tutorials/platform/index
   tutorials/plugins/index
   tutorials/rendering/index
   tutorials/scripting/index
   tutorials/shaders/index
   tutorials/ui/index
   tutorials/xr/index


.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Chi tiết về Engine
   :name: sec-engine-details

   engine_details/architecture/index
   engine_details/engine_api/index
   engine_details/development/index
   engine_details/editor/index
   engine_details/class_reference/index
   engine_details/file_formats/index


.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Cộng đồng
   :name: sec-community

   community/asset_library/index
   community/asset_store/index
   community/channels
   community/tutorials


.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Tra cứu Class
   :name: sec-class-ref

   classes/index

.. _`original English one`: https://docs.godotengine.org/en/stable
.. _`Weblate`: https://hosted.weblate.org/projects/godot-engine/godot-docs
.. _`GitHub repository`: https://github.com/godotengine/godot-docs/issues
.. _`translate the documentation`: https://hosted.weblate.org/engage/godot-engine/
.. _`Godot Contributors Chat`: https://chat.godotengine.org/
