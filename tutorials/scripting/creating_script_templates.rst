.. _doc_creating_script_templates:

Tạo template script
===================

Godot cung cấp cách sử dụng các template script như trong ``Script Create Dialog`` khi tạo script mới:

.. image:: img/script_create_dialog_templates.webp

Trình editor cung cấp một bộ template script tích hợp sẵn, nhưng bạn cũng có thể tạo template mới và đặt chúng làm mặc định, cả ở cấp project lẫn cấp editor.

Template được liên kết với một loại node cụ thể, vì vậy khi tạo script, bạn chỉ thấy các template tương ứng với node đó hoặc một trong các loại node cha của nó. Ví dụ, nếu đang tạo script cho một CharacterBody3D, bạn chỉ thấy các template được định nghĩa cho CharacterBody3D, Node3D hoặc Node.

Xác định vị trí các template
----------------------------

Có hai nơi để quản lý template.

Template do editor định nghĩa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Các template này khả dụng trên toàn cục trong mọi project. Vị trí của các template này được xác định theo từng OS:

-  Windows: ``%APPDATA%\Godot\script_templates\`` - Linux: ``$HOME/.config/godot/script_templates/`` - macOS: ``$HOME/Library/Application Support/Godot/script_templates/``

Nếu bạn nhận Godot từ một nguồn khác ngoài website chính thức, chẳng hạn như Steam, thư mục này có thể nằm ở vị trí khác. Bạn có thể tìm thư mục bằng Godot editor. Đi tới ``Editor > Open Editor Data/Settings Folder`` và một thư mục sẽ được mở trong trình duyệt file; bên trong thư mục đó là thư mục ``script_templates``.

Template do project định nghĩa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đường dẫn mặc định để tìm template là thư mục ``res://script_templates/``. Có thể thay đổi đường dẫn này bằng cách cấu hình project setting
:ref:`Editor > Script > Templates Search Path<class_ProjectSettings_property_editor/script/templates_search_path>`,
cả bằng code và trong editor.

Nếu không tìm thấy thư mục ``script_templates`` trong project, thư mục đó sẽ được bỏ qua.

Tổ chức và đặt tên template
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cả template do editor định nghĩa và template do project định nghĩa đều được tổ chức như sau:

::

  template_path/node_type/file.extension

trong đó:

* ``template_path`` là một trong 2 vị trí được thảo luận trong hai phần trước.

* ``node_type`` là node mà template sẽ áp dụng cho (ví dụ: :ref:`Node <class_Node>` hoặc :ref:`CharacterBody3D <class_CharacterBody3D>`). Đây là **phân biệt chữ hoa chữ thường**. Nếu một script không nằm trong thư mục ``node_type`` phù hợp, script đó sẽ không được phát hiện.

* ``file`` là tên tùy chỉnh bạn có thể chọn cho template (ví dụ: ``platformer_movement`` hoặc ``smooth_camera``).

* ``extension`` cho biết template sẽ áp dụng cho ngôn ngữ nào (phải là ``gd`` đối với GDScript hoặc ``cs`` đối với C#).

Ví dụ:

-  ``script_templates/Node/smooth_camera.gd`` - ``script_templates/CharacterBody3D/platformer_movement.gd``

Hành vi mặc định và cách ghi đè
-------------------------------

Theo mặc định:

* tên của template giống với tên file (bỏ phần mở rộng và được định dạng đẹp)

* mô tả để trống

* thụt lề bằng dấu cách được đặt là 4

* template sẽ không được đặt làm mặc định cho node tương ứng


Bạn có thể tùy chỉnh hành vi này bằng cách thêm các meta header ở đầu file, như sau:

.. tabs::

 .. code-tab:: gdscript GDScript

  # meta-name: Platformer movement
  # meta-description: Predefined movement for classical platformers
  # meta-default: true
  # meta-space-indent: 4

 .. code-tab:: csharp

  // meta-name: Platformer movement
  // meta-description: Predefined movement for classical platformers
  // meta-default: true
  // meta-space-indent: 4


Trong trường hợp này, tên sẽ được đặt là "Platformer movement", cùng với phần mô tả tùy chỉnh đã cho, và template sẽ được đặt làm template mặc định cho node trong thư mục nơi nó được lưu.

Đây là ví dụ về việc sử dụng template tùy chỉnh ở cấp editor và cấp project:

.. image:: img/script_create_dialog_custom_templates.webp

.. note:: The script templates have the same extension as the regular script
          file. Điều này có thể khiến parser của script coi các template đó là những script thực tế trong project. Để tránh điều này, hãy đảm bảo bỏ qua thư mục chứa chúng bằng cách tạo một file ``.gdignore`` trống. Thư mục này sẽ không còn hiển thị trong filesystem của project, nhưng bạn vẫn có thể chỉnh sửa các template bằng text editor bên ngoài bất kỳ lúc nào.

.. tip::

    Theo mặc định, mọi file C# bên trong thư mục project đều được đưa vào quá trình biên dịch. Phải loại trừ thủ công các template script khỏi project C# để tránh lỗi build. Xem `Exclude files from the build <https://learn.microsoft.com/en-us/visualstudio/msbuild/how-to-exclude-files-from-the-build>`_ trong tài liệu Microsoft.

Bạn có thể tạo các template ở cấp editor có cùng cấp độ với template dành riêng cho project, cũng như có cùng tên với template tích hợp sẵn; tất cả chúng sẽ được hiển thị trong hộp thoại tạo script mới.

Template mặc định
-----------------

Để ghi đè template mặc định, hãy tạo một template tùy chỉnh ở cấp editor hoặc cấp project bên trong thư mục ``Node`` (hoặc một loại cụ thể hơn, nếu chỉ muốn ghi đè một subtype), rồi bắt đầu file bằng header ``meta-default: true``.

Tại cùng một thời điểm, chỉ có thể đặt một template làm mặc định cho cùng một loại node.

Các template ``Default`` cho Node cơ bản, cả GDScript và C#, được hiển thị ở đây để bạn có thể dùng làm cơ sở tạo các template khác:

.. tabs::

 .. code-tab:: gdscript GDScript

    # meta-description: Base template for Node with default Godot cycle methods

    extends _BASE_


    # Called when the node enters the scene tree for the first time.
    func _ready() -> void:
        pass # Replace with function body.


    # Called every frame. 'delta' is the elapsed time since the previous frame.
    func _process(delta: float) -> void:
        pass


 .. code-tab:: csharp

    // meta-description: Base template for Node with default Godot cycle methods

    using _BINDINGS_NAMESPACE_;
    using System;

    public partial class _CLASS_ : _BASE_
    {
        // Called when the node enters the scene tree for the first time.
        public override void _Ready()
        {
        }

        // Called every frame. 'delta' is the elapsed time since the previous frame.
        public override void _Process(double delta)
        {
        }
    }

Godot editor cung cấp một bộ template tích hợp sẵn hữu ích dành riêng cho node, chẳng hạn như ``basic_movement`` cho cả :ref:`CharacterBody2D <class_CharacterBody2D>` và
:ref:`CharacterBody3D <class_CharacterBody3D>` and ``plugin`` for
:ref:`EditorPlugin <class_EditorPlugin>`.

Danh sách placeholder của template
----------------------------------

Phần sau mô tả đầy đủ danh sách các placeholder tích hợp sẵn hiện đang được triển khai.

Placeholder cơ sở
~~~~~~~~~~~~~~~~~

+--------------------------+----------------------------------------------------+
| Placeholder              | Description                                        |
+==========================+====================================================+
| ``_BINDINGS_NAMESPACE_`` | The name of the Godot namespace (used in C# only). |
+--------------------------+----------------------------------------------------+
| ``_CLASS_``              | The name of the new class.                         |
+--------------------------+----------------------------------------------------+
| ``_CLASS_SNAKE_CASE_``   | The name of the new class as ``snake_case``        |
|                          | (used in GDScript only).                           |
+--------------------------+----------------------------------------------------+
| ``_BASE_``               | The base type a new script inherits from.          |
+--------------------------+----------------------------------------------------+
| ``_TS_``                 | Indentation placeholder. The exact type and number |
|                          | of whitespace characters used for indentation is   |
|                          | determined by the ``text_editor/indent/type`` and  |
|                          | ``text_editor/indent/size`` settings in the        |
|                          | :ref:`EditorSettings <class_EditorSettings>`       |
|                          | respectively. Can be overridden by the             |
|                          | ``meta-space-indent`` header on the template.      |
+--------------------------+----------------------------------------------------+

Placeholder kiểu
~~~~~~~~~~~~~~~~

Trong Godot 3.x, từng có các placeholder cho type hint của GDScript, được thay thế mỗi khi template được dùng để tạo script mới, chẳng hạn như: ``%INT_TYPE%``, ``%STRING_TYPE%``, ``%FLOAT_TYPE%`` hoặc ``%VOID_RETURN%``.

Các placeholder này không còn hoạt động trong Godot 4.x, nhưng nếu setting ``text_editor/completion/add_type_hints`` từ
:ref:`EditorSettings <class_EditorSettings>` is disabled, type hints
đối với parameter và kiểu trả về sẽ được tự động loại bỏ đối với một số kiểu cơ sở:

* ``int`` * ``String`` * ``Array[String]`` * ``float`` * ``void`` * ``:=`` sẽ được chuyển đổi thành ``=``
