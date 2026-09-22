.. _doc_optimizing_for_size:

Tối ưu hóa bản build để giảm kích thước
=======================================

.. highlight:: shell

Lý do
-----

Đôi khi, bạn nên tối ưu hóa bản build để giảm kích thước thay vì tăng tốc độ. Điều này có nghĩa là không biên dịch các hàm không được sử dụng trong engine, đồng thời sử dụng các compiler flag cụ thể để góp phần giảm kích thước bản build. Các tình huống phổ biến bao gồm tạo bản build cho nền tảng di động và Web.

Tutorial này nhằm cung cấp cái nhìn tổng quan về các phương pháp khác nhau để tạo binary nhỏ hơn. Trước khi tiếp tục, bạn nên đọc các tutorial trước về cách biên dịch Godot cho từng nền tảng.

Các tùy chọn dưới đây được liệt kê từ quan trọng nhất (tiết kiệm nhiều dung lượng nhất) đến ít quan trọng nhất (tiết kiệm ít dung lượng nhất).

Loại bỏ symbol khỏi binary
--------------------------

- **Tiết kiệm dung lượng:** Rất cao
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Có

Nếu bạn build binary cho Windows (MinGW), Linux hoặc macOS từ source, hãy nhớ loại bỏ debug symbol khỏi binary bằng cách cài đặt package ``strip`` từ bản phân phối của bạn, sau đó chạy:

::

    strip path/to/godot.binary

Trên Windows, ``strip.exe`` được tích hợp trong hầu hết các thiết lập toolchain MinGW.

Thao tác này sẽ giảm kích thước binary đã biên dịch xuống khoảng từ 5× đến 10×. Nhược điểm là các crash backtrace sẽ không còn cung cấp thông tin chính xác (vốn hữu ích để tìm nguyên nhân crash).
:ref:`C++ profiler <doc_using_cpp_profilers>` cũng sẽ không còn hiển thị được tên hàm (điều này không ảnh hưởng đến GDScript profiler tích hợp sẵn).

.. note::

    Lệnh trên sẽ không hoạt động với binary Windows được biên dịch bằng MSVC và các nền tảng như Android và Web. Thay vào đó, hãy truyền ``debug_symbols=no`` trên dòng lệnh SCons khi biên dịch.

Biên dịch với link-time optimization
------------------------------------

- **Tiết kiệm dung lượng:** Cao
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Có

Bật link-time optimization sẽ tạo ra các binary hiệu quả hơn, cả về hiệu năng lẫn kích thước file. Tính năng này hoạt động bằng cách loại bỏ các template function trùng lặp và code không được sử dụng. Hiện tại, tính năng này có thể được sử dụng với compiler GCC và MSVC:

::

    scons target=template_release lto=full

Việc linking sẽ chậm hơn nhiều và tiêu tốn nhiều RAM hơn khi bật tùy chọn này, vì vậy chỉ nên sử dụng tùy chọn này cho các bản build release. Bạn cần có ít nhất 8 GB RAM khả dụng để linking thành công khi bật LTO. Vì hệ điều hành và các chương trình sẽ chiếm một phần RAM, trên thực tế, bạn cần lắp đặt 12 GB RAM trong hệ thống (tốt nhất là 16 GB) để biên dịch Godot khi bật LTO.

Tối ưu hóa để giảm kích thước thay vì tăng tốc độ
-------------------------------------------------

- **Tiết kiệm dung lượng:** Cao
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Có, nhưng chỉ với các bản build Web

Có thể biên dịch Godot bằng các tối ưu hóa cho kích thước (thay vì tốc độ). Để bật tùy chọn này, hãy đặt flag ``optimize`` thành ``size``:

::

    scons target=template_release optimize=size

Một số nền tảng như WebAssembly đã sử dụng chế độ này theo mặc định.

Godot 4.5 giới thiệu tùy chọn ``size_extra``, tùy chọn này có thể tiếp tục giảm kích thước.

::

    scons target=template_release optimize=size_extra

Phát hiện các tính năng được sử dụng trong project hiện tại và vô hiệu hóa các tính năng không được sử dụng
-----------------------------------------------------------------------------------------------------------

- **Tiết kiệm dung lượng:** Trung bình đến cao tùy thuộc vào project
- **Độ khó:** Dễ đến trung bình tùy thuộc vào project
- **Được thực hiện trong các bản build chính thức:** Không

Godot có một tool :ref:`doc_engine_compilation_configuration_editor` có thể phát hiện các tính năng được sử dụng trong project hiện tại và tạo build profile. Sau khi được lưu, build profile này có thể được truyền cho SCons khi biên dịch các custom export template:

::

    scons target=template_release build_profile=/path/to/profile.gdbuild

Lưu ý rằng với một số project, việc phát hiện tính năng có thể quá nghiêm ngặt và vô hiệu hóa những tính năng thực sự cần thiết khi runtime. Điều này có thể xảy ra nếu một số tính năng được sử dụng theo cách khiến việc sử dụng chúng không thể được phát hiện một cách tĩnh (chẳng hạn như một script được tạo theo thủ tục và chạy khi runtime).

Có thể vô hiệu hóa các tính năng cụ thể hơn bằng cách làm theo các phần bên dưới, nhưng hãy nhớ rằng nhiều tính năng trong số đó được tự động phát hiện bởi trình phát hiện cấu hình biên dịch engine.

Vô hiệu hóa advanced text server
--------------------------------

- **Tiết kiệm dung lượng:** Cao
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Không

Theo mặc định, Godot sử dụng advanced text server với hỗ trợ cho các tính năng sau:

- Dàn chữ từ phải sang trái và các script phức tạp, cần thiết để viết các ngôn ngữ như tiếng Ả Rập và tiếng Do Thái.
- Ligature của font và các tính năng OpenType (chẳng hạn như chữ hoa nhỏ, phân số và số 0 có gạch chéo).

Godot cung cấp một fallback text server không được biên dịch theo mặc định. Text server này có thể được sử dụng như một lựa chọn nhẹ hơn cho advanced text server mặc định:

::

    scons target=template_release module_text_server_adv_enabled=no module_text_server_fb_enabled=yes

Nếu project của bạn chỉ cần hỗ trợ các ngôn ngữ dựa trên chữ Latin, Hy Lạp và Cyrillic, fallback text server sẽ đáp ứng đủ.

Máy chủ văn bản dự phòng này cũng có thể xử lý lượng văn bản lớn nhanh hơn máy chủ văn bản nâng cao. Điều này khiến máy chủ văn bản dự phòng trở thành lựa chọn phù hợp cho các dự án mobile/web.

.. note::

    Hãy nhớ luôn truyền ``module_text_server_fb_enabled=yes`` khi sử dụng ``module_text_server_adv_enabled=no``. Nếu không, binary đã biên dịch sẽ không chứa bất kỳ máy chủ văn bản nào, nghĩa là hoàn toàn không có văn bản nào được hiển thị khi chạy dự án.

Tắt 3D
------

- **Tiết kiệm dung lượng:** Trung bình
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Không

Đối với các game 2D, việc cung cấp toàn bộ engine 3D thường không có ý nghĩa. Vì vậy, có một build flag để tắt tính năng này:

::

    scons target=template_release disable_3d=yes

Phải tắt Tools để sử dụng flag này, vì editor không được thiết kế để hoạt động khi không có hỗ trợ 3D. Khi tắt, kích thước binary có thể giảm khoảng 15%.

Tắt các đối tượng GUI nâng cao
------------------------------

- **Tiết kiệm dung lượng:** Trung bình
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Không

Hầu hết các game nhỏ không cần những GUI control phức tạp như Tree, ItemList, TextEdit hoặc GraphEdit. Có thể tắt chúng bằng build flag:

::

    scons target=template_release disable_advanced_gui=yes

Sau đây là toàn bộ những gì sẽ bị tắt:

- :ref:`class_AcceptDialog`
- :ref:`class_CharFXTransform`
- :ref:`class_CodeEdit`
- :ref:`class_CodeHighlighter`
- :ref:`class_ColorPicker`
- :ref:`class_ColorPickerButton`
- :ref:`class_ConfirmationDialog`
- :ref:`class_FileDialog`
- :ref:`class_FoldableContainer`
- :ref:`class_FoldableGroup`
- :ref:`class_GraphEdit`
- :ref:`class_GraphElement`
- :ref:`class_GraphFrame`
- :ref:`class_GraphNode`
- :ref:`class_HSplitContainer`
- :ref:`class_MenuBar`
- :ref:`class_MenuButton`
- :ref:`class_OptionButton`
- :ref:`class_PopupMenu` (sẽ khiến tất cả popup menu không khả dụng trong code đối với các class sử dụng chúng, chẳng hạn như :ref:`class_LineEdit`, mặc dù các class đó vẫn khả dụng)
- :ref:`class_RichTextEffect`
- :ref:`class_RichTextLabel`
- :ref:`class_SpinBox`
- :ref:`class_SplitContainer`
- :ref:`class_SubViewportContainer`
- :ref:`class_SyntaxHighlighter`
- :ref:`class_TextEdit`
- :ref:`class_Tree`
- :ref:`class_TreeItem`
- :ref:`class_VSplitContainer`

Tắt các physics engine
----------------------

- **Tiết kiệm dung lượng:** Thấp đến trung bình
- **Độ khó:** Dễ
- **Được thực hiện trong các bản build chính thức:** Không

Nếu dự án 3D của bạn sử dụng Jolt Physics, bạn có thể tắt GodotPhysics3D lúc compile vì nó sẽ không bao giờ được sử dụng:

::

    scons target=template_release module_godot_physics_3d_enabled=no

Ngược lại, nếu dự án 3D của bạn sử dụng GodotPhysics3D, bạn có thể tắt Jolt Physics lúc compile:

::

    scons target=template_release module_jolt_enabled=no

Nếu dự án của bạn sử dụng kết xuất 3D nhưng không sử dụng physics (hoặc kết xuất 2D nhưng không sử dụng physics), bạn cũng có thể tắt hoàn toàn physics 2D hoặc 3D. Hầu hết các dự án 3D đều có thể tận dụng điều này, vì chúng không sử dụng physics 2D:

::

    scons target=template_release disable_physics_2d=yes

::

    scons target=template_release disable_physics_3d=yes

Tắt các module không cần thiết
------------------------------

- **Tiết kiệm dung lượng:** Rất thấp đến trung bình, tùy thuộc vào module
- **Độ khó:** Trung bình đến khó, tùy thuộc vào module
- **Được thực hiện trong các bản build chính thức:** Không

Nhiều chức năng của Godot được cung cấp dưới dạng module. Bạn có thể xem danh sách các module bằng lệnh sau:

::

    scons --help

Danh sách các module có thể tắt sẽ xuất hiện cùng với tất cả tùy chọn build. Nếu đang phát triển một game 2D đơn giản, bạn có thể tắt nhiều module trong số đó:

::

    scons target=template_release module_astcenc_enabled=no module_basis_universal_enabled=no module_bcdec_enabled=no module_bmp_enabled=no module_camera_enabled=no module_csg_enabled=no module_dds_enabled=no module_enet_enabled=no module_etcpak_enabled=no module_fbx_enabled=no module_gltf_enabled=no module_gridmap_enabled=no module_hdr_enabled=no module_interactive_music_enabled=no module_jsonrpc_enabled=no module_ktx_enabled=no module_mbedtls_enabled=no module_meshoptimizer_enabled=no module_mp3_enabled=no module_mobile_vr_enabled=no module_msdfgen_enabled=no module_multiplayer_enabled=no module_noise_enabled=no module_navigation_2d_enabled=no module_navigation_3d_enabled=no module_ogg_enabled=no module_openxr_enabled=no module_raycast_enabled=no module_regex_enabled=no module_svg_enabled=no module_tga_enabled=no module_theora_enabled=no module_tinyexr_enabled=no module_upnp_enabled=no module_vhacd_enabled=no module_vorbis_enabled=no module_webrtc_enabled=no module_websocket_enabled=no module_webxr_enabled=no module_zip_enabled=no

Nếu cách này không phù hợp với trường hợp sử dụng của bạn, hãy xem lại danh sách module và xác định những module bạn thực sự vẫn cần cho game (chẳng hạn như bạn có thể muốn giữ các module liên quan đến networking, hỗ trợ regex, ``mp3``/``ogg``/``vorbis`` để phát nhạc hoặc ``theora`` để phát video).

Ngoài ra, bạn có thể cung cấp danh sách các module bị tắt bằng cách tạo ``custom.py`` tại thư mục gốc của mã nguồn, với nội dung tương tự như sau:

.. code-block:: python
    :caption: custom.py

    module_astcenc_enabled = "no"
    module_basis_universal_enabled = "no"
    module_bcdec_enabled = "no"
    module_bmp_enabled = "no"
    module_camera_enabled = "no"
    module_csg_enabled = "no"
    module_dds_enabled = "no"
    module_enet_enabled = "no"
    module_etcpak_enabled = "no"
    module_fbx_enabled = "no"
    module_gltf_enabled = "no"
    module_gridmap_enabled = "no"
    module_hdr_enabled = "no"
    module_interactive_music_enabled = "no"
    module_jsonrpc_enabled = "no"
    module_ktx_enabled = "no"
    module_mbedtls_enabled = "no"
    module_meshoptimizer_enabled = "no"
    module_mp3_enabled = "no"
    module_mobile_vr_enabled = "no"
    module_msdfgen_enabled = "no"
    module_multiplayer_enabled = "no"
    module_noise_enabled = "no"
    module_navigation_2d_enabled = "no"
    module_navigation_3d_enabled = "no"
    module_ogg_enabled = "no"
    module_openxr_enabled = "no"
    module_raycast_enabled = "no"
    module_regex_enabled = "no"
    module_svg_enabled = "no"
    module_tga_enabled = "no"
    module_theora_enabled = "no"
    module_tinyexr_enabled = "no"
    module_upnp_enabled = "no"
    module_vhacd_enabled = "no"
    module_vorbis_enabled = "no"
    module_webrtc_enabled = "no"
    module_websocket_enabled = "no"
    module_webxr_enabled = "no"
    module_zip_enabled = "no"

.. seealso::

    :ref:`doc_overriding_build_options`.

Tối ưu hóa việc phân phối dự án
-------------------------------

Desktop
~~~~~~~

.. note::

    Phần này chỉ liên quan khi phân phối các tệp trên một nền tảng desktop không tự thực hiện việc nén hoặc đóng gói. Vì vậy, hướng dẫn này phù hợp khi bạn phân phối các tệp ZIP trên itch.io hoặc GitHub Releases.

    Các nền tảng như Steam đã áp dụng cơ chế nén riêng, nên ngay từ đầu bạn không cần tạo tệp ZIP để phân phối các tệp.

Ngoài ra, bạn có thể xem xét việc tối ưu hóa chính quá trình phân phối dự án. Việc này có thể thực hiện ngay cả khi không biên dịch lại export template.

`7-Zip <https://7-zip.org/>`__ có thể được sử dụng để tạo các tệp ZIP hiệu quả hơn thông thường, đồng thời vẫn tương thích với mọi trình giải nén ZIP (bao gồm trình giải nén tích hợp sẵn của Windows). Với một dự án lớn, dung lượng ZIP có thể giảm hàng chục megabyte so với trình nén ZIP thông thường, mặc dù mức tiết kiệm trung bình nằm trong khoảng 1-5 MB. Việc tạo tệp ZIP này sẽ mất nhiều thời gian hơn bình thường, nhưng tốc độ giải nén sẽ nhanh như mọi tệp ZIP khác.

Khi sử dụng GUI của 7-Zip, bạn thực hiện việc này bằng cách tạo tệp ZIP với chế độ nén Ultra. Khi sử dụng command line, bạn thực hiện bằng lệnh sau:

::

    7z a -mx9 my_project.zip folder_containing_executable_and_pck

Web
~~~

Bật tính năng nén gzip hoặc Brotli cho tất cả các loại tệp trong bản xuất web (đặc biệt là ``.wasm`` và ``.pck``) có thể giảm đáng kể kích thước tải xuống, giúp thời gian tải nhanh hơn, đặc biệt trên các kết nối chậm.

Việc tạo các tệp gzip hoặc Brotli được nén trước với mức nén cao có thể còn hiệu quả hơn, miễn là web server được cấu hình để phân phối các tệp đó khi chúng tồn tại. Khi được hỗ trợ, nên ưu tiên Brotli thay cho gzip vì Brotli có khả năng giảm kích thước tệp nhiều hơn.

Xem :ref:`doc_exporting_for_web_serving_the_files` để biết hướng dẫn.
