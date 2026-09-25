.. _doc_creating_script_templates:

Tạo các template script
=======================

Godot cung cấp cách sử dụng các template script như minh họa trong ``Script Create Dialog`` khi tạo script mới:

.. image:: img/script_create_dialog_templates.webp

Trình editor cung cấp một tập hợp các template script dựng sẵn, nhưng bạn cũng có thể tạo template mới và đặt chúng làm mặc định, theo từng project cũng như ở cấp editor.

Các template được liên kết với một kiểu node cụ thể, vì vậy khi tạo script, bạn chỉ thấy các template tương ứng với node đó hoặc một trong các kiểu cha của nó. Ví dụ: nếu đang tạo script cho CharacterBody3D, bạn chỉ thấy các template được định nghĩa cho CharacterBody3D, Node3D hoặc Node.

Định vị các template
--------------------

Có hai vị trí có thể quản lý template.

Template do editor định nghĩa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các template này khả dụng trên toàn cục trong mọi project. Vị trí của các template này được xác định theo từng hệ điều hành:

-  Windows: ``%APPDATA%\Godot\script_templates\``
-  Linux: ``$HOME/.config/godot/script_templates/``
-  macOS: ``$HOME/Library/Application Support/Godot/script_templates/``

Nếu bạn tải Godot từ nơi khác ngoài website chính thức, chẳng hạn như Steam, thư mục này có thể nằm ở vị trí khác. Bạn có thể tìm thư mục bằng Godot editor. Đi tới ``Editor > Open Editor Data/Settings Folder`` và một thư mục sẽ được mở trong trình duyệt file; bên trong thư mục đó là thư mục ``script_templates``.

Template do project định nghĩa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đường dẫn mặc định để tìm template là thư mục ``res://script_templates/``. Bạn có thể thay đổi đường dẫn bằng cách cấu hình project setting
:ref:`Editor > Script > Templates Search Path <class_ProjectSettings_property_editor/script/templates_search_path>`, thông qua cả code lẫn editor.

Nếu không tìm thấy thư mục ``script_templates`` trong project, thư mục đó sẽ bị bỏ qua.

Tổ chức và đặt tên template
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cả template do editor định nghĩa và template do project định nghĩa đều được tổ chức như sau:

::

  template_path/node_type/file.extension

trong đó:

* ``template_path`` là một trong 2 vị trí được đề cập trong hai phần trước.

* ``node_type`` là node mà template sẽ áp dụng (ví dụ: :ref:`Node <class_Node>` hoặc :ref:`CharacterBody3D <class_CharacterBody3D>`). Thành phần này **phân biệt chữ hoa chữ thường**. Nếu script không nằm trong thư mục ``node_type`` phù hợp, script sẽ không được phát hiện.

* ``file`` là tên tùy chỉnh bạn có thể chọn cho template (ví dụ: ``platformer_movement`` hoặc ``smooth_camera``).

* ``extension`` cho biết template sẽ áp dụng cho ngôn ngữ nào (phải là ``gd`` đối với GDScript hoặc ``cs`` đối với C#).

Ví dụ:

-  ``script_templates/Node/smooth_camera.gd``
-  ``script_templates/CharacterBody3D/platformer_movement.gd``

Hành vi mặc định và cách ghi đè
-------------------------------

Theo mặc định:

* tên của template giống với tên file (bỏ phần mở rộng và được định dạng lại)ด้วย

* mô tả để trống

* thụt lề bằng khoảng trắng được đặt là 4

* template sẽ không được đặt làm mặc định cho node tương ứng


Bạn có thể tùy chỉnh hành vi này bằng cách thêm các header meta ở đầu file, như sau:

.. tabs::

 .. code-tab:: gdscript GDScript

  # meta-name: Di chuyển kiểu Platformer
  # meta-description: Chuyển động được định nghĩa sẵn cho các platformer cổ điển
  # meta-default: true
  # meta-space-indent: 4

 .. code-tab:: csharp

  // meta-name: Di chuyển kiểu Platformer
  // meta-description: Chuyển động được định nghĩa sẵn cho các platformer cổ điển
  // meta-default: true
  // meta-space-indent: 4


Trong trường hợp này, tên sẽ được đặt thành "Di chuyển kiểu Platformer", kèm theo mô tả tùy chỉnh đã cho, và template sẽ được đặt làm template mặc định cho node trong thư mục nơi template được lưu.

Đây là một ví dụ về việc sử dụng template tùy chỉnh ở cấp editor và project:

.. image:: img/script_create_dialog_custom_templates.webp

.. note:: Các template script có cùng phần mở rộng với các file script thông thường. Điều này có thể khiến trình phân tích script coi các template đó là script thực tế trong một project. Để tránh điều này, hãy đảm bảo bỏ qua thư mục chứa chúng bằng cách tạo một file ``.gdignore`` trống. Thư mục sẽ không còn hiển thị trong hệ thống file của project, nhưng bạn vẫn có thể chỉnh sửa các template bằng trình soạn thảo văn bản bên ngoài bất cứ lúc nào.

.. tip::

    Theo mặc định, mọi file C# bên trong thư mục project đều được đưa vào quá trình biên dịch. Bạn phải loại trừ thủ công các template script khỏi project C# để tránh lỗi build. Xem `Exclude files from the build <https://learn.microsoft.com/en-us/visualstudio/msbuild/how-to-exclude-files-from-the-build>`_ trong tài liệu Microsoft.

Bạn có thể tạo các template ở cấp editor có cùng cấp độ với template dành riêng cho project, cũng như có cùng tên với template dựng sẵn; tất cả chúng sẽ được hiển thị trong hộp thoại tạo script mới.

Template mặc định
-----------------

Để ghi đè template mặc định, hãy tạo một template tùy chỉnh ở cấp editor hoặc project bên trong thư mục ``Node`` (hoặc một kiểu cụ thể hơn nếu chỉ muốn ghi đè một kiểu con), rồi bắt đầu file bằng header ``meta-default: true``.

Tại một thời điểm, chỉ có thể đặt một template làm mặc định cho cùng một kiểu node.

Các template ``Default`` cho Node cơ bản, dành cho cả GDScript và C#, được hiển thị ở đây để bạn có thể dùng chúng làm cơ sở tạo các template khác:

.. tabs::

 .. code-tab:: gdscript GDScript

    # meta-description: Template cơ sở cho Node với các phương thức chu kỳ Godot mặc định

    extends _BASE_


    # Được gọi khi node lần đầu tiên đi vào scene tree.
    func _ready() -> void:
        pass # Thay thế bằng phần thân hàm.


    # Được gọi ở mỗi frame. 'delta' là thời gian đã trôi qua kể từ frame trước đó.
    func _process(delta: float) -> void:
        pass


 .. code-tab:: csharp

    // meta-description: Template cơ sở cho Node với các phương thức chu kỳ mặc định của Godot

    using _BINDINGS_NAMESPACE_;
    using System;

    public partial class _CLASS_ : _BASE_
    {
        // Được gọi khi node đi vào scene tree lần đầu tiên.
        public override void _Ready()
        {
        }

        // Được gọi ở mỗi frame. 'delta' là thời gian đã trôi qua kể từ frame trước đó.
        public override void _Process(double delta)
        {
        }
    }

Trình chỉnh sửa Godot cung cấp một tập hợp các template tích hợp hữu ích dành riêng cho từng node, chẳng hạn như ``basic_movement`` cho cả :ref:`CharacterBody2D <class_CharacterBody2D>` và
:ref:`CharacterBody3D <class_CharacterBody3D>` và ``plugin`` cho
:ref:`EditorPlugin <class_EditorPlugin>`.

Danh sách placeholder của template
----------------------------------

Phần sau mô tả danh sách đầy đủ các placeholder của template tích hợp hiện đang được triển khai.

Placeholder cơ sở
~~~~~~~~~~~~~~~~~

+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Placeholder              | Mô tả                                                                                                                                                                                       |
+==========================+=============================================================================================================================================================================================+
| ``_BINDINGS_NAMESPACE_`` | Tên của namespace Godot (chỉ được sử dụng trong C#).                                                                                                                                        |
+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``_CLASS_``              | Tên của class mới.                                                                                                                                                                          |
+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``_CLASS_SNAKE_CASE_``   | Tên của class mới dưới dạng ``snake_case`` (chỉ được sử dụng trong GDScript).                                                                                                               |
+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``_BASE_``               | Kiểu cơ sở mà script mới kế thừa.                                                                                                                                                           |
+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``_TS_``                 | Placeholder thụt lề. Kiểu và số lượng ký tự khoảng trắng chính xác được sử dụng để thụt lề được xác định bởi các thiết lập ``text_editor/indent/type`` và ``text_editor/indent/size`` trong |
|                          | :ref:`EditorSettings <class_EditorSettings>` tương ứng. Có thể ghi đè bằng header ``meta-space-indent`` trong template.                                                                     |
+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Placeholder kiểu
~~~~~~~~~~~~~~~~

Trong Godot 3.x từng có các placeholder cho type hint của GDScript, được thay thế mỗi khi template được dùng để tạo script mới, chẳng hạn như: ``%INT_TYPE%``, ``%STRING_TYPE%``, ``%FLOAT_TYPE%`` hoặc ``%VOID_RETURN%``.

Các placeholder này không còn hoạt động trong Godot 4.x, nhưng nếu thiết lập ``text_editor/completion/add_type_hints`` trong
:ref:`EditorSettings <class_EditorSettings>` bị tắt, type hint cho các tham số và kiểu trả về sẽ tự động bị xóa đối với một số kiểu cơ sở:

* ``int``
* ``String``
* ``Array[String]``
* ``float``
* ``void``
* ``:=`` sẽ được chuyển đổi thành ``=``

.. _`Exclude files from the build`: https://learn.microsoft.com/en-us/visualstudio/msbuild/how-to-exclude-files-from-the-build
