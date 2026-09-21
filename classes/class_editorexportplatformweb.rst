:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/platform/web/doc_classes/EditorExportPlatformWeb.xml.

.. _class_EditorExportPlatformWeb:

EditorExportPlatformWeb
=======================

**Kế thừa:** :ref:`EditorExportPlatform<class_EditorExportPlatform>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Exporter cho Web.

.. rst-class:: classref-introduction-group

Mô tả
-----

Web exporter tùy chỉnh cách xử lý web build. Trong cửa sổ "Export" của editor, nó được tạo khi thêm một preset "Web" mới.

\ **Lưu ý:** Godot trên Web được render bên trong thẻ ``<canvas>``. Thông thường, canvas không thể được định vị hoặc thay đổi kích thước thủ công, nhưng mặt khác, nó hoạt động như :ref:`Window<class_Window>` chính của ứng dụng.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Exporting for the Web <../tutorials/export/exporting_for_web>`

- :doc:`Web documentation index <../tutorials/platform/web/index>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`custom_template/debug<class_EditorExportPlatformWeb_property_custom_template/debug>`                                                                         |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`custom_template/release<class_EditorExportPlatformWeb_property_custom_template/release>`                                                                     |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`html/canvas_resize_policy<class_EditorExportPlatformWeb_property_html/canvas_resize_policy>`                                                                 |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`html/custom_html_shell<class_EditorExportPlatformWeb_property_html/custom_html_shell>`                                                                       |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`html/experimental_virtual_keyboard<class_EditorExportPlatformWeb_property_html/experimental_virtual_keyboard>`                                               |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`html/export_icon<class_EditorExportPlatformWeb_property_html/export_icon>`                                                                                   |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`html/focus_canvas_on_start<class_EditorExportPlatformWeb_property_html/focus_canvas_on_start>`                                                               |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`html/head_include<class_EditorExportPlatformWeb_property_html/head_include>`                                                                                 |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`   | :ref:`progressive_web_app/background_color<class_EditorExportPlatformWeb_property_progressive_web_app/background_color>`                                           |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`progressive_web_app/display<class_EditorExportPlatformWeb_property_progressive_web_app/display>`                                                             |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`progressive_web_app/enabled<class_EditorExportPlatformWeb_property_progressive_web_app/enabled>`                                                             |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`progressive_web_app/ensure_cross_origin_isolation_headers<class_EditorExportPlatformWeb_property_progressive_web_app/ensure_cross_origin_isolation_headers>` |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`progressive_web_app/icon_144x144<class_EditorExportPlatformWeb_property_progressive_web_app/icon_144x144>`                                                   |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`progressive_web_app/icon_180x180<class_EditorExportPlatformWeb_property_progressive_web_app/icon_180x180>`                                                   |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`progressive_web_app/icon_512x512<class_EditorExportPlatformWeb_property_progressive_web_app/icon_512x512>`                                                   |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`progressive_web_app/offline_page<class_EditorExportPlatformWeb_property_progressive_web_app/offline_page>`                                                   |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`progressive_web_app/orientation<class_EditorExportPlatformWeb_property_progressive_web_app/orientation>`                                                     |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`threads/emscripten_pool_size<class_EditorExportPlatformWeb_property_threads/emscripten_pool_size>`                                                           |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`       | :ref:`threads/godot_pool_size<class_EditorExportPlatformWeb_property_threads/godot_pool_size>`                                                                     |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`variant/extensions_support<class_EditorExportPlatformWeb_property_variant/extensions_support>`                                                               |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`variant/thread_support<class_EditorExportPlatformWeb_property_variant/thread_support>`                                                                       |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`vram_texture_compression/for_desktop<class_EditorExportPlatformWeb_property_vram_texture_compression/for_desktop>`                                           |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`vram_texture_compression/for_mobile<class_EditorExportPlatformWeb_property_vram_texture_compression/for_mobile>`                                             |
   +-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorExportPlatformWeb_property_custom_template/debug:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/debug** :ref:`🔗<class_EditorExportPlatformWeb_property_custom_template/debug>`

Đường dẫn tệp đến export template tùy chỉnh được dùng cho các debug build. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_custom_template/release:

.. rst-class:: classref-property

:ref:`String<class_String>` **custom_template/release** :ref:`🔗<class_EditorExportPlatformWeb_property_custom_template/release>`

Đường dẫn tệp đến export template tùy chỉnh được dùng cho các release build. Nếu để trống, template mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/canvas_resize_policy:

.. rst-class:: classref-property

:ref:`int<class_int>` **html/canvas_resize_policy** :ref:`🔗<class_EditorExportPlatformWeb_property_html/canvas_resize_policy>`

Xác định cách canvas sẽ được Godot thay đổi kích thước.

- **None:** Canvas không được tự động thay đổi kích thước.

- **Project:** Kích thước canvas phụ thuộc vào :ref:`ProjectSettings<class_ProjectSettings>`.

- **Adaptive:** Canvas được tự động thay đổi kích thước để vừa với phần lớn trang web nhất có thể.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/custom_html_shell:

.. rst-class:: classref-property

:ref:`String<class_String>` **html/custom_html_shell** :ref:`🔗<class_EditorExportPlatformWeb_property_html/custom_html_shell>`

Trang HTML tùy chỉnh bao bọc web build đã export. Nếu để trống, HTML shell mặc định sẽ được sử dụng.

Để biết thêm thông tin, hãy xem tutorial :doc:`Customizing HTML5 Shell <../tutorials/platform/web/customizing_html5_shell>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/experimental_virtual_keyboard:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **html/experimental_virtual_keyboard** :ref:`🔗<class_EditorExportPlatformWeb_property_html/experimental_virtual_keyboard>`

**Experimental:** Thuộc tính này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Nếu ``true``, nhúng hỗ trợ bàn phím ảo vào trang web, bàn phím này sẽ hiển thị khi cần trên các thiết bị màn hình cảm ứng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/export_icon:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **html/export_icon** :ref:`🔗<class_EditorExportPlatformWeb_property_html/export_icon>`

Nếu ``true``, icon của project sẽ được dùng làm favicon cho trang web của ứng dụng này.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/focus_canvas_on_start:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **html/focus_canvas_on_start** :ref:`🔗<class_EditorExportPlatformWeb_property_html/focus_canvas_on_start>`

Nếu ``true``, canvas sẽ được focus ngay khi ứng dụng được tải, nếu cửa sổ trình duyệt đã được focus.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_html/head_include:

.. rst-class:: classref-property

:ref:`String<class_String>` **html/head_include** :ref:`🔗<class_EditorExportPlatformWeb_property_html/head_include>`

Các thẻ HTML bổ sung cần đưa vào bên trong ``<head>``, chẳng hạn như các thẻ ``<meta>``.

\ **Lưu ý:** Bạn không cần thêm thẻ ``<title>``, vì thẻ này được tự động thêm dựa trên tên project.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/background_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **progressive_web_app/background_color** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/background_color>`

Màu nền được sử dụng phía sau web application.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/display:

.. rst-class:: classref-property

:ref:`int<class_int>` **progressive_web_app/display** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/display>`

`display mode <https://developer.mozilla.org/en-US/docs/Web/Manifest/display/>`__ cần sử dụng cho progressive web application này. Các trình duyệt và nền tảng khác nhau có thể không hoạt động giống nhau.

- **Fullscreen:** Hiển thị app ở chế độ toàn màn hình và ẩn tất cả các thành phần UI của trình duyệt.

- **Standalone:** Hiển thị app trong một cửa sổ riêng và ẩn tất cả các thành phần UI của trình duyệt.

- **Minimal UI:** Hiển thị app trong một cửa sổ riêng và chỉ hiển thị các thành phần UI của trình duyệt dùng cho việc điều hướng.

- **Browser:** Hiển thị app như một trang web thông thường.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **progressive_web_app/enabled** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/enabled>`

Nếu ``true``, biến web build này thành một `progressive web application <https://en.wikipedia.org/wiki/Progressive_web_app>`__ (PWA).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/ensure_cross_origin_isolation_headers:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **progressive_web_app/ensure_cross_origin_isolation_headers** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/ensure_cross_origin_isolation_headers>`

Khi được bật, progressive web app sẽ đảm bảo mỗi request có các header cross-origin isolation (COEP/COOP).

Điều này có thể đơn giản hóa việc thiết lập để phục vụ game đã export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/icon_144x144:

.. rst-class:: classref-property

:ref:`String<class_String>` **progressive_web_app/icon_144x144** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/icon_144x144>`

Đường dẫn tệp đến icon nhỏ nhất cho web application này. Nếu chưa được định nghĩa, mặc định là icon của project.

\ **Lưu ý:** Nếu icon không có kích thước 144×144, nó sẽ được tự động thay đổi kích thước cho build cuối cùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/icon_180x180:

.. rst-class:: classref-property

:ref:`String<class_String>` **progressive_web_app/icon_180x180** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/icon_180x180>`

Đường dẫn tệp đến icon nhỏ cho web application này. Nếu chưa được định nghĩa, mặc định là icon của project.

\ **Lưu ý:** Nếu icon không có kích thước 180×180, nó sẽ được tự động thay đổi kích thước cho build cuối cùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/icon_512x512:

.. rst-class:: classref-property

:ref:`String<class_String>` **progressive_web_app/icon_512x512** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/icon_512x512>`

Đường dẫn tệp đến icon lớn nhất cho web application này. Nếu chưa được định nghĩa, mặc định là icon của project.

\ **Lưu ý:** Nếu icon không có kích thước 512×512, nó sẽ được tự động thay đổi kích thước cho build cuối cùng.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/offline_page:

.. rst-class:: classref-property

:ref:`String<class_String>` **progressive_web_app/offline_page** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/offline_page>`

Trang sẽ hiển thị nếu server lưu trữ trang không khả dụng. Trang này được lưu trên máy của client.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_progressive_web_app/orientation:

.. rst-class:: classref-property

:ref:`int<class_int>` **progressive_web_app/orientation** :ref:`🔗<class_EditorExportPlatformWeb_property_progressive_web_app/orientation>`

Hướng hiển thị được sử dụng khi web application chạy trên thiết bị di động.

- **Any:** Không ép buộc hướng hiển thị nào.

- **Landscape:** Ép bố cục ngang (rộng hơn chiều cao).

- **Portrait:** Ép bố cục dọc (cao hơn chiều rộng).

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_threads/emscripten_pool_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **threads/emscripten_pool_size** :ref:`🔗<class_EditorExportPlatformWeb_property_threads/emscripten_pool_size>`

Số lượng thread mà emscripten sẽ cấp phát khi khởi động. Giá trị nhỏ hơn sẽ cấp phát ít thread hơn và tiêu tốn ít tài nguyên hệ thống hơn, nhưng bạn có thể gặp rủi ro hết thread trong pool và cần cấp phát thêm thread tại runtime, điều này có thể gây deadlock.

\ **Lưu ý:** Một số trình duyệt có giới hạn cứng về số lượng thread có thể được cấp phát, vì vậy tốt nhất nên thận trọng và giữ giá trị này ở mức thấp.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_threads/godot_pool_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **threads/godot_pool_size** :ref:`🔗<class_EditorExportPlatformWeb_property_threads/godot_pool_size>`

Ghi đè kích thước mặc định của :ref:`WorkerThreadPool<class_WorkerThreadPool>`. Thiết lập này được sử dụng khi kích thước :ref:`ProjectSettings.threading/worker_pool/max_threads<class_ProjectSettings_property_threading/worker_pool/max_threads>` được đặt thành ``-1`` (đây là giá trị mặc định). Kích thước này phải nhỏ hơn :ref:`threads/emscripten_pool_size<class_EditorExportPlatformWeb_property_threads/emscripten_pool_size>`, nếu không có thể xảy ra deadlock.

Khi sử dụng thread, kích thước này cần đủ lớn để đáp ứng các tính năng phụ thuộc vào một thread riêng, chẳng hạn như :ref:`ProjectSettings.physics/2d/run_on_separate_thread<class_ProjectSettings_property_physics/2d/run_on_separate_thread>` hoặc :ref:`ProjectSettings.rendering/driver/threads/thread_model<class_ProjectSettings_property_rendering/driver/threads/thread_model>`. Nhìn chung, tốt nhất nên đảm bảo giá trị này ít nhất là ``4`` và ít nhất ``2`` hoặc ``3`` nhỏ hơn :ref:`threads/emscripten_pool_size<class_EditorExportPlatformWeb_property_threads/emscripten_pool_size>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_variant/extensions_support:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **variant/extensions_support** :ref:`🔗<class_EditorExportPlatformWeb_property_variant/extensions_support>`

Nếu ``true``, bật hỗ trợ :ref:`GDExtension<class_GDExtension>` cho web build này.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_variant/thread_support:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **variant/thread_support** :ref:`🔗<class_EditorExportPlatformWeb_property_variant/thread_support>`

Nếu ``true``, game đã export sẽ hỗ trợ thread. Tính năng này yêu cầu `a "cross-origin isolated" website <https://web.dev/articles/coop-coep>`__, có thể khó thiết lập và bị giới hạn vì lý do bảo mật (chẳng hạn như không thể giao tiếp với các website bên thứ ba).

Nếu ``false``, game đã export sẽ không hỗ trợ thread. Do đó, game dễ gặp các vấn đề về hiệu năng và âm thanh hơn, nhưng chỉ yêu cầu chạy trên một website HTTPS.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_vram_texture_compression/for_desktop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **vram_texture_compression/for_desktop** :ref:`🔗<class_EditorExportPlatformWeb_property_vram_texture_compression/for_desktop>`

Nếu ``true``, cho phép tối ưu hóa texture cho desktop thông qua thuật toán S3TC/BPTC.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPlatformWeb_property_vram_texture_compression/for_mobile:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **vram_texture_compression/for_mobile** :ref:`🔗<class_EditorExportPlatformWeb_property_vram_texture_compression/for_mobile>`

Nếu ``true``, cho phép tối ưu hóa texture cho mobile thông qua thuật toán ETC2/ASTC.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
