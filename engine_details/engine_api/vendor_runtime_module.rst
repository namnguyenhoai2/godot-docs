.. _doc_vendor_runtime_module:

Mô-đun Runtime của nhà cung cấp
===============================

Mô-đun Runtime của nhà cung cấp là một :ref:`Godot module <doc_custom_modules_in_cpp>` chỉ được áp dụng tại runtime trong một project đang chạy. Mô-đun này được tạo như một :ref:`custom C++ module <doc_custom_modules_in_cpp>` thông thường, nhưng được đóng gói bằng :ref:`editor plugin <doc_making_plugins>` để giúp chức năng mà nó cung cấp dễ dàng truy cập và sử dụng trong một project Godot *stock*.

Dùng để làm gì?
---------------

Các mô-đun runtime của nhà cung cấp cung cấp cho developer quyền truy cập vào các tối ưu hóa, tính năng và/hoặc nền tảng dành riêng cho nhà cung cấp trong project đang chạy của họ.

Điều này mang lại lợi ích cho các nhà cung cấp, những bên có thể cung cấp công nghệ của mình cho tất cả developer, đồng thời cải thiện và hoàn thiện chúng một cách nhanh chóng, lặp lại và không ma sát. Điều này cũng mang lại lợi ích cho developer và người dùng, những bên có thể truy cập và sử dụng nhiều công nghệ đa dạng của nhà cung cấp để cải thiện game của mình.

Tạo mô-đun runtime của nhà cung cấp
-----------------------------------

Tạo export template
~~~~~~~~~~~~~~~~~~~

Hãy đảm bảo bạn làm theo :ref:`instructions for creating a custom C++ module <doc_creating_custom_modules_in_cpp>`.

Vì đây là một mô-đun runtime có chức năng chỉ được truy cập từ project đang chạy, bạn phải tạo một export template cho mọi nền tảng mà bạn dự định hỗ trợ. Xem các trang :ref:`Compiling <toc-devel-compiling>` để biết thêm thông tin.

Tạo editor plugin wrapper
~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi các export template được tạo, bạn phải tạo một editor plugin để đóng gói chúng và giúp người dùng cuối dễ dàng truy cập thông qua `Godot Asset Store <https://store.godotengine.org/>`_.

Làm theo :ref:`these instructions <doc_making_plugins_template>` để bắt đầu tạo plugin. Script plugin cơ sở của bạn sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin


    func _enter_tree():
        # Phần khởi tạo plugin được đặt tại đây.
        pass


    func _exit_tree():
        # Phần dọn dẹp plugin được đặt tại đây.
        pass


Bước tiếp theo là định nghĩa và khởi tạo một instance :ref:`EditorExportPlugin<class_EditorExportPlugin>`. Instance :ref:`EditorExportPlugin<class_EditorExportPlugin>` được dùng để móc nối vào quy trình export và thay thế các export template mặc định bằng những template được tạo từ mô-đun runtime của nhà cung cấp.

Sử dụng mã template editor plugin cơ sở ở trên, một cách triển khai mẫu sẽ có dạng như sau:

.. code-block:: gdscript

    @tool
    extends EditorPlugin

    # Một thành viên của class dùng để lưu editor export plugin trong suốt vòng đời của nó.
    var export_plugin: VRMExportPlugin

    func _enter_tree():
        # Phần khởi tạo plugin được đặt tại đây.
        export_plugin = VRMExportPlugin.new()
        add_export_plugin(export_plugin)


    func _exit_tree():
        # Phần dọn dẹp plugin được đặt tại đây.
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

    Phần này trình bày những kiến thức cơ bản để bọc và cung cấp quyền truy cập vào một mô-đun runtime của nhà cung cấp thông qua editor plugin, nhưng editor plugin còn có nhiều chức năng hơn có thể được sử dụng để tùy chỉnh editor sâu hơn. Bạn có thể :ref:`explore and leverage those functionalities <toc-tutorials-plugins>` để cải thiện trải nghiệm người dùng cho mô-đun runtime của nhà cung cấp.
