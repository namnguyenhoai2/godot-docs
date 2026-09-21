:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorPaths.xml.

.. _class_EditorPaths:

EditorPaths
===========

**Kế thừa:** :ref:`Object<class_Object>`

Singleton chỉ dành cho editor, trả về các đường dẫn đến nhiều thư mục và tệp dữ liệu dành riêng cho từng hệ điều hành.

.. rst-class:: classref-introduction-group

Mô tả
-----

Singleton chỉ dành cho editor này trả về các đường dẫn dành riêng cho từng hệ điều hành đến nhiều thư mục và tệp dữ liệu. Có thể sử dụng singleton này trong các editor plugin để đảm bảo tệp được lưu đúng vị trí trên mỗi hệ điều hành.

\ **Lưu ý:** Singleton này không thể truy cập trong các project đã export. Việc cố gắng truy cập singleton này trong một project đã export sẽ dẫn đến lỗi script vì singleton này sẽ không được khai báo. Để ngăn lỗi script trong các project đã export, hãy sử dụng :ref:`Engine.has_singleton()<class_Engine_method_has_singleton>` để kiểm tra xem singleton có khả dụng trước khi sử dụng hay không.

\ **Lưu ý:** Trên nền tảng Linux/BSD, Godot tuân theo `XDG Base Directory Specification <https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html>`__. Bạn có thể override các biến môi trường theo đặc tả để thay đổi đường dẫn dữ liệu của editor và project.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Đường dẫn tệp trong các project Godot <../tutorials/io/data_paths>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_cache_dir<class_EditorPaths_method_get_cache_dir>`\ (\ ) |const|                       |
   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_config_dir<class_EditorPaths_method_get_config_dir>`\ (\ ) |const|                     |
   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_data_dir<class_EditorPaths_method_get_data_dir>`\ (\ ) |const|                         |
   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_project_settings_dir<class_EditorPaths_method_get_project_settings_dir>`\ (\ ) |const| |
   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_self_contained_file<class_EditorPaths_method_get_self_contained_file>`\ (\ ) |const|   |
   +-----------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`is_self_contained<class_EditorPaths_method_is_self_contained>`\ (\ ) |const|               |
   +-----------------------------+--------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorPaths_method_get_cache_dir:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_cache_dir**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_get_cache_dir>`

Trả về đường dẫn tuyệt đối đến thư mục cache của người dùng. Thư mục này nên được dùng cho dữ liệu tạm thời có thể xóa an toàn bất cứ khi nào editor đóng (chẳng hạn như thumbnail của resource được tạo tự động).

\ **Đường dẫn mặc định theo nền tảng:**\

.. code:: text

    - Windows: %LOCALAPPDATA%\Godot\
    - macOS: ~/Library/Caches/Godot/
    - Linux: ~/.cache/godot/

.. rst-class:: classref-item-separator

----

.. _class_EditorPaths_method_get_config_dir:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_config_dir**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_get_config_dir>`

Trả về đường dẫn tuyệt đối đến thư mục cấu hình của người dùng. Thư mục này nên được dùng cho các tệp cấu hình *persistent* của người dùng.

\ **Đường dẫn mặc định theo nền tảng:**\

.. code:: text

    - Windows: %APPDATA%\Godot\                    (same as `get_data_dir()`)
    - macOS: ~/Library/Application Support/Godot/  (same as `get_data_dir()`)
    - Linux: ~/.config/godot/

.. rst-class:: classref-item-separator

----

.. _class_EditorPaths_method_get_data_dir:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_data_dir**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_get_data_dir>`

Trả về đường dẫn tuyệt đối đến thư mục dữ liệu của người dùng. Thư mục này nên được dùng cho các tệp dữ liệu *persistent* của người dùng, chẳng hạn như các export template đã cài đặt.

\ **Đường dẫn mặc định theo nền tảng:**\

.. code:: text

    - Windows: %APPDATA%\Godot\                    (same as `get_config_dir()`)
    - macOS: ~/Library/Application Support/Godot/  (same as `get_config_dir()`)
    - Linux: ~/.local/share/godot/

.. rst-class:: classref-item-separator

----

.. _class_EditorPaths_method_get_project_settings_dir:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_project_settings_dir**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_get_project_settings_dir>`

Trả về đường dẫn tương đối đến các thiết lập editor cho project này. Thông thường, đường dẫn này là ``"res://.godot/editor"``. Mọi project đều có một thư mục con duy nhất bên trong đường dẫn thiết lập, nơi lưu các thiết lập editor dành riêng cho project.

.. rst-class:: classref-item-separator

----

.. _class_EditorPaths_method_get_self_contained_file:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_self_contained_file**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_get_self_contained_file>`

Trả về đường dẫn tuyệt đối đến tệp self-contained khiến instance editor Godot hiện tại được xem là self-contained. Trả về một chuỗi rỗng nếu instance editor Godot hiện tại không ở chế độ self-contained. Xem thêm :ref:`is_self_contained()<class_EditorPaths_method_is_self_contained>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorPaths_method_is_self_contained:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_self_contained**\ (\ ) |const| :ref:`🔗<class_EditorPaths_method_is_self_contained>`

Trả về ``true`` nếu editor được đánh dấu là self-contained, ngược lại trả về ``false``. Khi bật chế độ self-contained, các tệp cấu hình, dữ liệu và cache của người dùng được lưu trong thư mục ``editor_data/`` bên cạnh binary của editor. Điều này giúp việc sử dụng portable dễ dàng hơn và đảm bảo editor Godot giảm thiểu việc ghi tệp bên ngoài thư mục của chính nó. Chế độ self-contained không khả dụng cho các project đã export.

Có thể bật chế độ self-contained bằng cách tạo một tệp có tên ``._sc_`` hoặc ``_sc_`` trong cùng thư mục với binary của editor hoặc macOS .app bundle khi editor không đang chạy. Xem thêm :ref:`get_self_contained_file()<class_EditorPaths_method_get_self_contained_file>`.

\ **Lưu ý:** Trên macOS, cần xóa thủ công cờ quarantine trước khi sử dụng chế độ self-contained, xem `Running on macOS <https://docs.godotengine.org/en/stable/tutorials/export/running_on_macos.html>`__.

\ **Lưu ý:** Trên macOS, việc đặt ``_sc_`` hoặc bất kỳ tệp nào khác bên trong .app bundle sẽ làm hỏng chữ ký số và khiến bundle không còn portable; thay vào đó, hãy cân nhắc đặt tệp này trong cùng thư mục với .app bundle.

\ **Lưu ý:** Bản phát hành Godot trên Steam mặc định sử dụng chế độ self-contained.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
