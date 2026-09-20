.. _doc_project_settings:

Cài đặt dự án
=============

Có hàng chục cài đặt mà bạn có thể thay đổi để kiểm soát quá trình thực thi của một dự án, bao gồm các cài đặt về vật lý, kết xuất và cửa sổ. Bạn có thể thay đổi các cài đặt này trong cửa sổ **Project Settings**, từ code hoặc bằng cách chỉnh sửa thủ công tệp ``project.godot``. Bạn có thể xem danh sách đầy đủ các cài đặt trong
:ref:`ProjectSettings <class_ProjectSettings>` class.

Về mặt nội bộ, Godot lưu trữ các cài đặt của một dự án trong tệp ``project.godot``, một tệp văn bản thuần túy ở định dạng INI. Mặc dù tệp này dễ đọc đối với con người và thân thiện với hệ thống quản lý phiên bản, nhưng việc chỉnh sửa không thuận tiện lắm. Vì lý do đó, cửa sổ **Project Settings** được cung cấp để chỉnh sửa các cài đặt này. Để mở Project Settings, hãy chọn **Project > Project Settings** từ menu chính.

.. figure:: img/project_settings_basic.webp
    :align: center

    The Project Settings window

Cửa sổ **Project Settings** chủ yếu được dùng để thay đổi các cài đặt trong tab **General**. Ngoài ra, còn có các tab dành cho
:ref:`Input Map <doc_input_examples_input_map>`,
:ref:`Localization <doc_internationalizing_games>`,
:ref:`Globals <doc_singletons_autoload>`,
:ref:`Plugins <doc_installing_plugins_enabling_a_plugin>`, and
**Import Defaults**. Việc sử dụng các tab khác này được trình bày ở nơi khác.

Thay đổi cài đặt dự án
----------------------

Tab **General** của cửa sổ cài đặt dự án hoạt động tương tự inspector. Tab này hiển thị danh sách các cài đặt dự án mà bạn có thể thay đổi, giống như các thuộc tính trong inspector. Ở bên trái là danh sách các danh mục, cho phép bạn chọn các nhóm cài đặt liên quan. Bạn cũng có thể tìm kiếm một cài đặt cụ thể bằng trường **Filter Settings**.

Mỗi cài đặt đều có một giá trị mặc định. Bạn có thể đặt lại cài đặt về giá trị mặc định bằng cách nhấp vào nút **Reset** có biểu tượng mũi tên tròn bên cạnh mỗi thuộc tính.

Thay đổi cài đặt dự án từ code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sử dụng :ref:`set_setting() <class_ProjectSettings_method_set_setting>` để thay đổi giá trị của một cài đặt từ code:

.. tabs::
    .. code-tab:: gdscript GDScript

        ProjectSettings.set_setting("application/run/max_fps", 60)
        ProjectSettings.set_setting("display/window/size/mode", DisplayServer.WINDOW_MODE_WINDOWED)

    .. code-tab:: csharp

        ProjectSettings.SetSetting("application/run/max_fps", 60);
        ProjectSettings.SetSetting("display/window/size/mode", (int)DisplayServer.WindowMode.Windowed);

Tuy nhiên, nhiều cài đặt dự án chỉ được đọc một lần khi game khởi động. Sau đó, việc thay đổi cài đặt bằng ``set_setting()`` sẽ không có tác dụng. Thay vào đó, hầu hết các cài đặt đều có thuộc tính hoặc method tương ứng trên một runtime class như
:ref:`Engine <class_Engine>` or :ref:`DisplayServer <class_DisplayServer>`:

.. tabs::
    .. code-tab:: gdscript GDScript

        Engine.max_fps = 60
        DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_WINDOWED)

    .. code-tab:: csharp

        Engine.MaxFps = 60;
        DisplayServer.WindowSetMode(DisplayServer.WindowMode.Windowed);

Nhìn chung, các cài đặt dự án được sao chép trong runtime vào
:ref:`Engine <class_Engine>`, :ref:`PhysicsServer2D <class_PhysicsServer2D>`,
:ref:`PhysicsServer3D <class_PhysicsServer3D>`,
:ref:`RenderingServer <class_RenderingServer>`,
:ref:`Viewport <class_Viewport>`, or :ref:`Window <class_Window>` classes. In the
:ref:`ProjectSettings <class_ProjectSettings>` class reference, settings
liên kết đến thuộc tính hoặc method runtime tương đương của chúng.

Đọc cài đặt dự án
-----------------

Bạn có thể đọc các cài đặt dự án bằng
:ref:`get_setting() <class_ProjectSettings_method_get_setting>` or
:ref:`get_setting_with_override() <class_ProjectSettings_method_get_setting_with_override>`:

.. tabs::
    .. code-tab:: gdscript GDScript

        var max_fps = ProjectSettings.get_setting("application/run/max_fps")
        var window_mode = ProjectSettings.get_setting("display/window/size/mode")

    .. code-tab:: csharp

        int maxFps = (int)ProjectSettings.GetSetting("application/run/max_fps");
        var windowMode = (DisplayServer.WindowMode)(int)ProjectSettings.GetSetting("display/window/size/mode");

Vì nhiều cài đặt dự án chỉ được đọc một lần khi khởi động, giá trị trong cài đặt dự án có thể không còn chính xác. Trong những trường hợp này, tốt hơn là đọc giá trị từ thuộc tính hoặc method runtime tương đương:

.. tabs::
    .. code-tab:: gdscript GDScript

        var max_fps = Engine.max_fps
        var window_mode = DisplayServer.window_get_mode()

    .. code-tab:: csharp

        int maxFps = Engine.MaxFps;
        DisplayServer.WindowMode windowMode = DisplayServer.WindowGetMode();

Chỉnh sửa thủ công project.godot
--------------------------------

Bạn có thể mở tệp ``project.godot`` bằng trình soạn thảo văn bản và thay đổi thủ công các cài đặt dự án. Lưu ý rằng nếu tệp ``project.godot`` không có giá trị được lưu cho một cài đặt cụ thể, thì cài đặt đó được ngầm định sử dụng giá trị mặc định. Điều này có nghĩa là nếu bạn đang chỉnh sửa tệp thủ công, bạn có thể phải ghi cả tên cài đặt *và* giá trị.

Nhìn chung, bạn nên sử dụng cửa sổ Project Settings thay vì chỉnh sửa thủ công ``project.godot``.

Cài đặt dự án nâng cao
----------------------

.. figure:: img/project_settings_advanced.webp
    :align: center

    The advanced project settings

Theo mặc định, chỉ một số cài đặt dự án được hiển thị. Để xem tất cả cài đặt dự án, hãy bật công tắc **Advanced Settings**.
