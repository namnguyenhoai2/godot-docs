.. _doc_vendor_runtime_module:

Mô-đun runtime của nhà cung cấp
===============================

Mô-đun runtime của nhà cung cấp là một :ref:`Godot module <doc_custom_modules_in_cpp>` chỉ áp dụng trong runtime của một dự án đang chạy. Mô-đun này được tạo như một :ref:`custom C++ module <doc_custom_modules_in_cpp>` thông thường, nhưng được đóng gói bằng :ref:`editor plugin <doc_making_plugins>` để chức năng mà nó cung cấp có thể dễ dàng truy cập và sử dụng trong một dự án Godot *stock*.

Dùng để làm gì?
---------------

Các mô-đun runtime của nhà cung cấp cung cấp cho nhà phát triển quyền truy cập vào những tối ưu hóa, tính năng và/hoặc nền tảng dành riêng cho nhà cung cấp trong các dự án đang chạy của họ.

Điều này mang lại lợi ích cho các nhà cung cấp, những bên có thể cung cấp công nghệ của mình cho tất cả nhà phát triển, đồng thời cải thiện và hoàn thiện chúng theo cách nhanh chóng, lặp lại và không gặp trở ngại. Điều này cũng mang lại lợi ích cho các nhà phát triển và người dùng, những bên có thể truy cập và sử dụng nhiều loại công nghệ đa dạng từ các nhà cung cấp để cải thiện trò chơi của mình.

Tạo mô-đun runtime của nhà cung cấp
-----------------------------------

Tạo các export template
~~~~~~~~~~~~~~~~~~~~~~~

Hãy nhớ làm theo :ref:`instructions for creating a custom C++ module <doc_creating_custom_modules_in_cpp>`.

Vì đây là một mô-đun runtime có chức năng chỉ được truy cập từ dự án đang chạy, bạn phải tạo một export template cho mỗi nền tảng mà bạn dự định hỗ trợ. Hãy xem các trang :ref:`Compiling <toc-devel-compiling>` để biết thêm thông tin.

Tạo editor plugin wrapper
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi các export template được tạo, bạn phải tạo một editor plugin để đóng gói chúng và giúp người dùng cuối dễ dàng truy cập thông qua `Godot Asset Store <https://store.godotengine.org/>`_.

Làm theo :ref:`these instructions <doc_making_plugins_template>` để bắt đầu tạo plugin. Tập lệnh plugin cơ sở của bạn sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin


    func _enter_tree():
        # Initialization of the plugin goes here.
        pass


    func _exit_tree():
        # Clean-up of the plugin goes here.
        pass


Bước tiếp theo là định nghĩa và khởi tạo một thực thể :ref:`EditorExportPlugin<class_EditorExportPlugin>`. Thực thể :ref:`EditorExportPlugin<class_EditorExportPlugin>` được dùng để móc vào quy trình export và thay thế các export template mặc định bằng những template được tạo từ mô-đun runtime của nhà cung cấp.

Sử dụng mã mẫu editor plugin cơ sở ở trên, một cách triển khai mẫu sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin

    # A class member to hold the editor export plugin during its lifecycle.
    var export_plugin: VRMExportPlugin

    func _enter_tree():
        # Initialization of the plugin goes here.
        export_plugin = VRMExportPlugin.new()
        add_export_plugin(export_plugin)


    func _exit_tree():
        # Clean-up of the plugin goes here.
        remove_export_plugin(export_plugin)
        export_plugin = null


    class VRMExportPlugin extends EditorExportPlugin:
        var _path_to_debug_export_template = ""
        var _path_to_release_export_template = ""

        # Return true for all supported platforms.
        func _supports_platform(platform):
            return platform is EditorExportPlatformAndroid

        # Overrides the default export templates.
        func _get_export_options_overrides(platform):
            var overrides = {}
            if not _supports_platform(platform):
                return overrides

            # Overrides Android export preset's "custom_template" options.
            overrides["custom_template/debug"] = _path_to_debug_export_template
            overrides["custom_template/release"] = _path_to_release_export_template

            return overrides

        # Optional: specify additional export preset options to customize the export template.
        func _get_export_options(platform):
            pass

        func _get_name():
            return "VRM Plugin"


.. tip::

    Phần này trình bày những kiến thức cơ bản để bao bọc và cung cấp quyền truy cập vào một mô-đun runtime của nhà cung cấp thông qua editor plugin, nhưng editor plugin còn có nhiều chức năng khác có thể được sử dụng để tùy chỉnh trình soạn thảo hơn nữa. Bạn có thể :ref:`explore and leverage those functionalities <toc-tutorials-plugins>` để cải thiện trải nghiệm người dùng đối với mô-đun runtime của nhà cung cấp.
