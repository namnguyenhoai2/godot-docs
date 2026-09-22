.. _doc_vendor_runtime_module:

Module Runtime của nhà cung cấp
===============================

Module Runtime của nhà cung cấp là một :ref:`module Godot <doc_custom_modules_in_cpp>` chỉ được áp dụng trong runtime của một project đang chạy. Module này được tạo như một :ref:`module C++ tùy chỉnh <doc_custom_modules_in_cpp>` thông thường, nhưng được đóng gói bằng một :ref:`editor plugin <doc_making_plugins>` để chức năng mà module cung cấp có thể dễ dàng được truy cập và sử dụng trong một project Godot *nguyên bản*.

Dùng để làm gì?
---------------

Các module runtime của nhà cung cấp cho phép developer truy cập vào những tối ưu hóa, tính năng và/hoặc nền tảng dành riêng cho nhà cung cấp trong các project đang chạy của họ.

Điều này mang lại lợi ích cho các nhà cung cấp, những bên có thể cung cấp công nghệ của mình cho mọi developer, đồng thời cải tiến và hoàn thiện chúng theo cách nhanh chóng, lặp lại và không ma sát. Điều này cũng mang lại lợi ích cho developer và người dùng, những bên có thể truy cập và sử dụng nhiều loại công nghệ đa dạng của các nhà cung cấp để cải thiện game của mình.

Tạo module runtime của nhà cung cấp
-----------------------------------

Tạo export template
~~~~~~~~~~~~~~~~~~~

Hãy đảm bảo làm theo :ref:`hướng dẫn tạo module C++ tùy chỉnh <doc_creating_custom_modules_in_cpp>`.

Vì đây là một module runtime có chức năng chỉ nhằm được truy cập từ project đang chạy, bạn phải tạo một export template cho mọi nền tảng mà bạn dự định hỗ trợ. Xem các trang :ref:`Compiling <toc-devel-compiling>` để biết thêm thông tin.

Tạo editor plugin wrapper
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi tạo các export template, bạn phải tạo một editor plugin để đóng gói chúng và giúp người dùng cuối dễ dàng truy cập thông qua `Godot Asset Store <https://store.godotengine.org/>`_.

Hãy làm theo :ref:`các hướng dẫn này <doc_making_plugins_template>` để bắt đầu tạo plugin. Script plugin cơ sở của bạn sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin


    func _enter_tree():
        # Đặt phần khởi tạo plugin tại đây.
        pass


    func _exit_tree():
        # Đặt phần dọn dẹp plugin tại đây.
        pass


Bước tiếp theo là định nghĩa và khởi tạo một instance :ref:`EditorExportPlugin<class_EditorExportPlugin>`. Instance :ref:`EditorExportPlugin<class_EditorExportPlugin>` được dùng để móc vào quy trình export và thay thế các export template mặc định bằng những template được tạo từ module runtime của nhà cung cấp.

Sử dụng mã template editor plugin cơ sở ở trên, một cách triển khai mẫu sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin

    # Một thành viên của class để lưu editor export plugin trong suốt vòng đời của nó.
    var export_plugin: VRMExportPlugin

    func _enter_tree():
        # Đặt phần khởi tạo plugin tại đây.
        export_plugin = VRMExportPlugin.new()
        add_export_plugin(export_plugin)


    func _exit_tree():
        # Đặt phần dọn dẹp plugin tại đây.
        remove_export_plugin(export_plugin)
        export_plugin = null


    class VRMExportPlugin extends EditorExportPlugin:
        var _path_to_debug_export_template = ""
        var _path_to_release_export_template = ""

        # Trả về true cho tất cả nền tảng được hỗ trợ.
        func _supports_platform(platform):
            return platform is EditorExportPlatformAndroid

        # Ghi đè các export template mặc định.
        func _get_export_options_overrides(platform):
            var overrides = {}
            if not _supports_platform(platform):
                return overrides

            # Ghi đè các tùy chọn "custom_template" của Android export preset.
            overrides["custom_template/debug"] = _path_to_debug_export_template
            overrides["custom_template/release"] = _path_to_release_export_template

            return overrides

        # Tùy chọn: chỉ định các tùy chọn export preset bổ sung để tùy chỉnh export template.
        func _get_export_options(platform):
            pass

        func _get_name():
            return "VRM Plugin"


.. tip::

    Phần này trình bày những kiến thức cơ bản để bọc và cung cấp một module runtime của nhà cung cấp thông qua một editor plugin, nhưng editor plugin còn có nhiều chức năng hơn có thể được sử dụng để tùy chỉnh editor sâu hơn. Bạn có thể :ref:`khám phá và tận dụng các chức năng đó <toc-tutorials-plugins>` để cải thiện trải nghiệm người dùng cho module runtime của nhà cung cấp.

.. _`Godot Asset Store`: https://store.godotengine.org/
