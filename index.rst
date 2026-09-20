:allow_comments: False

Tài liệu Godot – nhánh *4.7*
============================

.. only:: not i18n

  .. note:: Godot's documentation is available in various languages and versions.
            Mở rộng bảng "Read the Docs" ở cuối thanh bên để xem danh sách.

.. only:: i18n

  .. note:: This documentation is translated from the `original English one
            <https://docs.godotengine.org/en/stable>`_ bởi các thành viên cộng đồng trên `Weblate <https://hosted.weblate.org/projects/godot-engine/godot-docs>`_.

            Tùy thuộc vào mức độ hoàn thành của nỗ lực dịch thuật, bạn có thể bắt gặp những đoạn văn hoặc toàn bộ trang vẫn còn bằng tiếng Anh. Bạn có thể giúp cộng đồng bằng cách cung cấp bản dịch mới hoặc xem xét các bản dịch hiện có trên Weblate.

            Hiện tại, bản dịch được bản địa hóa chỉ có sẵn cho nhánh "stable". Bạn vẫn có thể xem tài liệu tiếng Anh cho các phiên bản engine khác bằng bảng "Read the Docs" ở cuối thanh bên.

Chào mừng bạn đến với tài liệu chính thức của `Godot Engine <https://godotengine.org>`__, một game engine 2D và 3D miễn phí, mã nguồn mở và do cộng đồng phát triển! Nếu bạn mới làm quen với tài liệu này, chúng tôi khuyên bạn nên đọc
:ref:`introduction page <doc_about_intro>` to get an overview of what this
những gì tài liệu cung cấp.

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
            <strong>Tôi muốn tìm hiểu thêm về các chủ đề nâng cao trong Godot.</strong>
        </a>
        <a class="grid-item contribute-to-godot" href="https://contributing.godotengine.org/en/latest/index.html">
            Tôi biết cách sử dụng Godot,<br>
            <strong>Tôi muốn đóng góp cho Godot.</strong>
        </a>
    </div>
    <br>

Bạn cũng có thể sử dụng mục lục trong thanh bên để dễ dàng truy cập bất kỳ phần nào của tài liệu về chủ đề bạn quan tâm. Bạn cũng có thể sử dụng chức năng tìm kiếm ở góc trên bên trái.

Tham gia đóng góp
-----------------

Godot Engine là một dự án mã nguồn mở được phát triển bởi cộng đồng tình nguyện viên. Nhóm tài liệu luôn cần phản hồi và sự trợ giúp của bạn để cải thiện các tutorial và tài liệu tham chiếu class. Nếu bạn không hiểu điều gì đó hoặc không thể tìm thấy nội dung mình cần trong tài liệu, hãy giúp chúng tôi làm tài liệu tốt hơn bằng cách cho chúng tôi biết!

Gửi issue hoặc pull request trên `GitHub repository <https://github.com/godotengine/godot-docs/issues>`_, giúp chúng tôi `dịch tài liệu <https://hosted.weblate.org/engage/godot-engine/>`_ sang ngôn ngữ của bạn, hoặc trò chuyện với chúng tôi trên kênh ``#documentation`` trong `Godot Contributors Chat <https://chat.godotengine.org/>`_!

.. centered:: |weblate_widget|

Tài liệu ngoại tuyến
--------------------

Để xem tài liệu ngoại tuyến, bạn có thể tải xuống bản HTML (được cập nhật vào mỗi thứ Hai): `stable <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-stable.zip>`__, `latest <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-master.zip>`__, `3.6 <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-html-3.6.zip>`__. Giải nén tệp lưu trữ ZIP, sau đó mở ``index.html`` cấp cao nhất trong trình duyệt web.

Đối với thiết bị di động hoặc thiết bị đọc sách điện tử, bạn cũng có thể tải xuống bản ePub (được cập nhật vào mỗi thứ Hai): `stable <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-stable.zip>`__, `latest <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-master.zip>`__, `3.6 <https://nightly.link/godotengine/godot-docs/workflows/build_offline_docs/master/godot-docs-epub-3.6.zip>`__. Giải nén tệp lưu trữ ZIP, sau đó mở tệp ``GodotEngine.epub`` trong ứng dụng đọc sách điện tử.

.. Dưới đây là cây mục lục chính của trang web tài liệu. Cây này bị ẩn trên chính trang đó, nhưng tạo thành thanh bên để điều hướng.

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


.. Các phần bên dưới được chia thành hai nhóm. Trước tiên là các phần meta, bao quát những vấn đề chung. Bên dưới là danh sách các khu vực khác nhau của engine. Các phần này được sắp xếp theo thứ tự bảng chữ cái. Vui lòng giữ nguyên thứ tự đó.
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
