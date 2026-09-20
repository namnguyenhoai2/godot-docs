.. _doc_optimizing_for_size:

Tối ưu hóa bản build để giảm kích thước
=======================================

.. highlight:: shell

Lý do
-----

Đôi khi, bạn muốn tối ưu hóa bản build để giảm kích thước thay vì tăng tốc độ. Điều này có nghĩa là không biên dịch các hàm không được sử dụng từ engine, đồng thời sử dụng các cờ trình biên dịch cụ thể để giúp giảm kích thước bản build. Các trường hợp phổ biến bao gồm tạo bản build cho nền tảng di động và Web.

Hướng dẫn này nhằm cung cấp tổng quan về các phương pháp khác nhau để tạo một tệp nhị phân nhỏ hơn. Trước khi tiếp tục, bạn nên đọc các hướng dẫn trước về biên dịch Godot cho từng nền tảng.

Các tùy chọn dưới đây được liệt kê từ quan trọng nhất (tiết kiệm kích thước nhiều nhất) đến ít quan trọng nhất (tiết kiệm kích thước ít nhất).

Loại bỏ thông tin thừa khỏi tệp nhị phân
----------------------------------------

- **Mức tiết kiệm dung lượng:** Rất cao - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Có

Nếu bạn build tệp nhị phân cho Windows (MinGW), Linux hoặc macOS từ mã nguồn, hãy nhớ loại bỏ các ký hiệu gỡ lỗi khỏi tệp nhị phân bằng cách cài đặt gói ``strip`` từ bản phân phối của bạn, sau đó chạy:

::

    strip path/to/godot.binary

Trên Windows, ``strip.exe`` được tích hợp trong hầu hết các thiết lập toolchain MinGW.

Thao tác này sẽ giảm kích thước của các tệp nhị phân đã biên dịch từ 5× đến 10×. Nhược điểm là các thông tin truy nguyên lỗi khi crash sẽ không còn cung cấp thông tin chính xác (vốn hữu ích để xác định nguyên nhân crash).
:ref:`C++ profilers <doc_using_cpp_profilers>` will also no longer be able to display
tên hàm (điều này không ảnh hưởng đến trình phân tích hiệu năng GDScript tích hợp sẵn).

.. note::

    Lệnh trên sẽ không hoạt động với các tệp nhị phân Windows được biên dịch bằng MSVC và các nền tảng như Android và Web. Thay vào đó, hãy truyền ``debug_symbols=no`` trên dòng lệnh SCons khi biên dịch.

Biên dịch với tối ưu hóa tại thời điểm liên kết
-----------------------------------------------

- **Mức tiết kiệm dung lượng:** Cao - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Có

Bật tối ưu hóa tại thời điểm liên kết sẽ tạo ra các tệp nhị phân hiệu quả hơn, cả về hiệu năng lẫn kích thước tệp. Tùy chọn này hoạt động bằng cách loại bỏ các hàm template trùng lặp và mã không được sử dụng. Hiện có thể sử dụng với các trình biên dịch GCC và MSVC:

::

    scons target=template_release lto=full

Việc liên kết sẽ chậm hơn nhiều và tiêu tốn nhiều RAM hơn khi bật tùy chọn này, vì vậy chỉ nên sử dụng cho các bản build phát hành. Bạn cần có ít nhất 8 GB RAM trống để liên kết thành công khi bật LTO. Vì hệ điều hành và các chương trình sẽ sử dụng một phần RAM, trên thực tế, bạn cần cài đặt 12 GB RAM trong hệ thống (tốt nhất là 16 GB) để biên dịch Godot khi bật LTO.

Tối ưu hóa để giảm kích thước thay vì tăng tốc độ
-------------------------------------------------

- **Mức tiết kiệm dung lượng:** Cao - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Có, nhưng chỉ dành cho các bản build web

Có thể biên dịch Godot bằng các tùy chọn tối ưu hóa kích thước (thay vì tốc độ). Để bật tùy chọn này, hãy đặt cờ ``optimize`` thành ``size``:

::

    scons target=template_release optimize=size

Một số nền tảng như WebAssembly đã sử dụng chế độ này theo mặc định.

Godot 4.5 giới thiệu tùy chọn ``size_extra``, có thể tiếp tục giảm kích thước.

::

    scons target=template_release optimize=size_extra

Phát hiện các tính năng được sử dụng từ dự án hiện tại và vô hiệu hóa các tính năng không sử dụng
-------------------------------------------------------------------------------------------------

- **Mức tiết kiệm dung lượng:** Trung bình đến cao tùy thuộc vào dự án - **Độ khó:** Dễ đến trung bình tùy thuộc vào dự án - **Được thực hiện trong các bản build chính thức:** Không

Godot có một công cụ :ref:`doc_engine_compilation_configuration_editor` có thể phát hiện các tính năng được sử dụng trong dự án hiện tại và tạo một hồ sơ build. Sau khi được lưu, hồ sơ build này có thể được truyền cho SCons khi biên dịch các export template tùy chỉnh:

::

    scons target=template_release build_profile=/path/to/profile.gdbuild

Lưu ý rằng với một số dự án, việc phát hiện tính năng có thể quá mạnh tay và vô hiệu hóa các tính năng thực sự cần thiết khi chạy. Điều này có thể xảy ra nếu một số tính năng được sử dụng theo cách mà việc sử dụng chúng không thể được phát hiện tĩnh (chẳng hạn như một script được tạo theo thủ tục và chạy trong thời gian chạy).

Có thể vô hiệu hóa các tính năng cụ thể hơn bằng cách làm theo các phần bên dưới, nhưng hãy nhớ rằng nhiều tính năng trong số đó được tự động phát hiện bởi trình phát hiện cấu hình biên dịch engine.

Vô hiệu hóa máy chủ văn bản nâng cao
------------------------------------

- **Mức tiết kiệm dung lượng:** Cao - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Không

Theo mặc định, Godot sử dụng máy chủ văn bản nâng cao với khả năng hỗ trợ các tính năng sau:

- Dàn chữ từ phải sang trái và các script phức tạp, cần thiết để viết các ngôn ngữ như tiếng Ả Rập và tiếng Hebrew. - Các chữ ghép phông chữ và tính năng OpenType (chẳng hạn như chữ hoa nhỏ, phân số và số 0 có gạch chéo).

Godot cung cấp một máy chủ văn bản dự phòng, không được biên dịch theo mặc định. Máy chủ văn bản này có thể được sử dụng như một giải pháp thay thế nhẹ hơn cho máy chủ văn bản nâng cao mặc định:

::

    scons target=template_release module_text_server_adv_enabled=no module_text_server_fb_enabled=yes

Nếu bạn chỉ định hỗ trợ các ngôn ngữ dựa trên bảng chữ cái Latin, Hy Lạp và Cyrillic trong dự án của mình, máy chủ văn bản dự phòng sẽ đáp ứng đủ.

Máy chủ văn bản dự phòng này cũng có thể xử lý lượng văn bản lớn nhanh hơn máy chủ văn bản nâng cao. Điều này khiến máy chủ văn bản dự phòng phù hợp với các dự án di động/web.

.. note::

    Hãy nhớ luôn truyền ``module_text_server_fb_enabled=yes`` khi sử dụng ``module_text_server_adv_enabled=no``. Nếu không, tệp nhị phân đã biên dịch sẽ không chứa bất kỳ máy chủ văn bản nào, nghĩa là sẽ không có văn bản nào được hiển thị khi chạy dự án.

Vô hiệu hóa 3D
--------------

- **Mức tiết kiệm dung lượng:** Trung bình - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Không

Đối với các game 2D, việc có toàn bộ engine 3D thường không có ý nghĩa. Vì vậy, có một cờ build để vô hiệu hóa nó:

::

    scons target=template_release disable_3d=yes

Phải vô hiệu hóa Tools để sử dụng cờ này, vì editor không được thiết kế để hoạt động khi không có hỗ trợ 3D. Khi đó, kích thước tệp nhị phân có thể giảm khoảng 15%.

Vô hiệu hóa các đối tượng GUI nâng cao
--------------------------------------

- **Mức tiết kiệm dung lượng:** Trung bình - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Không

Hầu hết các game nhỏ không cần các điều khiển GUI phức tạp như Tree, ItemList, TextEdit hoặc GraphEdit. Có thể vô hiệu hóa chúng bằng một cờ build:

::

    scons target=template_release disable_advanced_gui=yes

Sau đây là toàn bộ những gì sẽ bị vô hiệu hóa:

- :ref:`class_AcceptDialog` - :ref:`class_CharFXTransform` - :ref:`class_CodeEdit` - :ref:`class_CodeHighlighter` - :ref:`class_ColorPicker` - :ref:`class_ColorPickerButton` - :ref:`class_ConfirmationDialog` - :ref:`class_FileDialog` - :ref:`class_FoldableContainer` - :ref:`class_FoldableGroup` - :ref:`class_GraphEdit` - :ref:`class_GraphElement` - :ref:`class_GraphFrame` - :ref:`class_GraphNode` - :ref:`class_HSplitContainer` - :ref:`class_MenuBar` - :ref:`class_MenuButton` - :ref:`class_OptionButton` - :ref:`class_PopupMenu` (sẽ khiến mọi menu bật lên không khả dụng trong mã đối với các lớp sử dụng chúng, như :ref:`class_LineEdit`, mặc dù các lớp đó vẫn khả dụng) - :ref:`class_RichTextEffect` - :ref:`class_RichTextLabel` - :ref:`class_SpinBox` - :ref:`class_SplitContainer` - :ref:`class_SubViewportContainer` - :ref:`class_SyntaxHighlighter` - :ref:`class_TextEdit` - :ref:`class_Tree` - :ref:`class_TreeItem` - :ref:`class_VSplitContainer`

Vô hiệu hóa các engine vật lý
-----------------------------

- **Mức tiết kiệm dung lượng:** Thấp đến trung bình - **Độ khó:** Dễ - **Được thực hiện trong các bản build chính thức:** Không

Nếu dự án 3D của bạn sử dụng Jolt Physics, bạn có thể vô hiệu hóa GodotPhysics3D trong thời gian biên dịch vì nó sẽ không bao giờ được sử dụng:

::

    scons target=template_release module_godot_physics_3d_enabled=no

Ngược lại, nếu dự án 3D của bạn sử dụng GodotPhysics3D, bạn có thể vô hiệu hóa Jolt Physics trong thời gian biên dịch:

::

    scons target=template_release module_jolt_enabled=no

Nếu dự án của bạn sử dụng kết xuất 3D nhưng không sử dụng vật lý (hoặc kết xuất 2D nhưng không sử dụng vật lý), bạn cũng có thể vô hiệu hóa hoàn toàn vật lý 2D hoặc 3D. Hầu hết các dự án 3D đều có thể tận dụng điều này, vì chúng không sử dụng vật lý 2D:

::

    scons target=template_release disable_physics_2d=yes

::

    scons target=template_release disable_physics_3d=yes

Vô hiệu hóa các module không cần thiết
--------------------------------------

- **Mức tiết kiệm dung lượng:** Rất thấp đến trung bình tùy thuộc vào module - **Độ khó:** Trung bình đến khó tùy thuộc vào module - **Được thực hiện trong các bản build chính thức:** Không

Nhiều chức năng của Godot được cung cấp dưới dạng module. Bạn có thể xem danh sách các module bằng lệnh sau:

::

    scons --help

Danh sách các module có thể vô hiệu hóa sẽ xuất hiện cùng với tất cả tùy chọn build. Nếu bạn đang phát triển một game 2D đơn giản, bạn có thể vô hiệu hóa khá nhiều module trong số đó:

::

    scons target=template_release module_astcenc_enabled=no module_basis_universal_enabled=no module_bcdec_enabled=no module_bmp_enabled=no module_camera_enabled=no module_csg_enabled=no module_dds_enabled=no module_enet_enabled=no module_etcpak_enabled=no module_fbx_enabled=no module_gltf_enabled=no module_gridmap_enabled=no module_hdr_enabled=no module_interactive_music_enabled=no module_jsonrpc_enabled=no module_ktx_enabled=no module_mbedtls_enabled=no module_meshoptimizer_enabled=no module_mp3_enabled=no module_mobile_vr_enabled=no module_msdfgen_enabled=no module_multiplayer_enabled=no module_noise_enabled=no module_navigation_2d_enabled=no module_navigation_3d_enabled=no module_ogg_enabled=no module_openxr_enabled=no module_raycast_enabled=no module_regex_enabled=no module_svg_enabled=no module_tga_enabled=no module_theora_enabled=no module_tinyexr_enabled=no module_upnp_enabled=no module_vhacd_enabled=no module_vorbis_enabled=no module_webrtc_enabled=no module_websocket_enabled=no module_webxr_enabled=no module_zip_enabled=no

Nếu cách này không phù hợp với trường hợp sử dụng của bạn, hãy xem lại danh sách module và xác định những module nào bạn thực sự vẫn cần cho game của mình (ví dụ: bạn có thể muốn giữ các module liên quan đến networking, hỗ trợ regex, ``mp3``/``ogg``/``vorbis`` để phát nhạc hoặc ``theora`` để phát video).

Ngoài ra, bạn có thể cung cấp danh sách các module bị vô hiệu hóa bằng cách tạo ``custom.py`` tại thư mục gốc của mã nguồn, với nội dung tương tự như sau:

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

Máy tính để bàn
~~~~~~~~~~~~~~~

.. note::

    Phần này chỉ liên quan khi phân phối các tệp trên một nền tảng máy tính để bàn không tự thực hiện việc nén hoặc đóng gói. Do đó, lời khuyên này phù hợp khi bạn phân phối các tệp lưu trữ ZIP trên itch.io hoặc GitHub Releases.

    Các nền tảng như Steam đã áp dụng cơ chế nén riêng, vì vậy ngay từ đầu bạn không cần tạo tệp lưu trữ ZIP để phân phối tệp.

Ngoài ra, bạn có thể tìm hiểu cách tối ưu hóa chính việc phân phối dự án. Điều này có thể thực hiện ngay cả khi không biên dịch lại export template.

Có thể sử dụng `7-Zip <https://7-zip.org/>`__ để tạo các tệp lưu trữ ZIP hiệu quả hơn thông thường mà vẫn tương thích với mọi trình giải nén ZIP (bao gồm cả trình giải nén tích hợp sẵn của Windows). Trong một dự án lớn, dung lượng ZIP có thể giảm hàng chục megabyte so với trình nén ZIP thông thường, mặc dù mức tiết kiệm trung bình nằm trong khoảng 1-5 MB. Việc tạo tệp lưu trữ ZIP này sẽ mất nhiều thời gian hơn thông thường, nhưng tốc độ giải nén sẽ nhanh tương đương mọi tệp lưu trữ ZIP khác.

Khi sử dụng giao diện GUI của 7-Zip, bạn thực hiện việc này bằng cách tạo một tệp lưu trữ ZIP với chế độ nén Ultra. Khi sử dụng dòng lệnh, bạn thực hiện việc này bằng lệnh sau:

::

    7z a -mx9 my_project.zip folder_containing_executable_and_pck

Web
~~~

Bật tính năng nén gzip hoặc Brotli cho tất cả loại tệp trong bản xuất web (đặc biệt là ``.wasm`` và ``.pck``) có thể giảm đáng kể dung lượng tải xuống, giúp thời gian tải nhanh hơn, đặc biệt khi kết nối chậm.

Việc tạo các tệp gzip hoặc Brotli được nén trước với mức nén cao có thể còn hiệu quả hơn, miễn là máy chủ web được cấu hình để cung cấp các tệp đó khi chúng tồn tại. Khi được hỗ trợ, nên ưu tiên Brotli hơn gzip vì Brotli có tiềm năng giảm dung lượng tệp lớn hơn.

Xem :ref:`doc_exporting_for_web_serving_the_files` để biết hướng dẫn.
