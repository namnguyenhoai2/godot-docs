.. _doc_engine_compilation_configuration_editor:

Sử dụng trình chỉnh sửa cấu hình biên dịch engine
=================================================

Godot đi kèm một tập hợp lớn các tính năng tích hợp sẵn. Mặc dù điều này rất tiện lợi, nhưng nó cũng khiến kích thước binary lớn hơn mức cần thiết, đặc biệt đối với các dự án chỉ sử dụng một phần nhỏ tập hợp tính năng này.

Để giúp giảm kích thước binary, bạn có thể biên dịch các export template tùy chỉnh với một số tính năng bị vô hiệu hóa. Nội dung này được mô tả chi tiết trong :ref:`doc_optimizing_for_size`. Tuy nhiên, việc xác định những tính năng nào cần bị vô hiệu hóa có thể khá tốn thời gian. Trình chỉnh sửa cấu hình biên dịch engine giải quyết vấn đề này bằng cách cung cấp một giao diện để dễ dàng xem và quản lý các tính năng, đồng thời có thể phát hiện những tính năng hiện đang được sử dụng trong dự án.

:menu:`Project > Tools > Engine Compilation Configuration Editor` cho phép bạn tạo và quản lý các build profile cho dự án Godot của mình.

Từ đây, bạn có hai lựa chọn:

- Xem danh sách và bỏ chọn thủ công các tính năng bạn không cần.
- Sử dụng nút :button:`Detect from Project` để tự động phát hiện các tính năng hiện đang được sử dụng trong dự án và vô hiệu hóa các tính năng không được sử dụng. Lưu ý rằng thao tác này sẽ ghi đè danh sách tính năng hiện có, vì vậy nếu bạn đã bỏ chọn thủ công một số mục, trạng thái của chúng sẽ được đặt lại dựa trên việc dự án có thực sự sử dụng tính năng đó hay không.

.. figure:: img/engine_compilation_configuration_editor_detect.webp
   :align: center
   :alt: Mở Trình chỉnh sửa cấu hình biên dịch Engine

   Mở Trình chỉnh sửa cấu hình biên dịch Engine

Sau khi bạn nhấp vào :button:`Detect from Project`, bước phát hiện dự án sẽ được thực hiện. Quá trình này có thể mất từ vài giây đến vài phút, tùy thuộc vào kích thước dự án. Khi quá trình phát hiện hoàn tất, bạn sẽ thấy danh sách tính năng được cập nhật với một số tính năng bị vô hiệu hóa:

.. figure:: img/engine_compilation_configuration_editor_detected.webp
   :align: center
   :alt: Danh sách tính năng được cập nhật sau khi sử dụng tính năng phát hiện (ví dụ từ bản demo platformer 3D)

   Danh sách tính năng được cập nhật sau khi sử dụng tính năng phát hiện (ví dụ từ bản demo platformer 3D)

.. warning::

    Việc bỏ chọn các tính năng trong hộp thoại này sẽ không trực tiếp làm giảm kích thước binary khi export. Vì chỉ có thể thực sự loại bỏ các tính năng khỏi binary tại thời điểm biên dịch, bạn vẫn cần biên dịch các export template tùy chỉnh với build profile đã chỉ định để thực sự tận dụng trình chỉnh sửa cấu hình biên dịch engine.

Bây giờ bạn có thể lưu build profile bằng cách nhấp vào **Save As** ở phía trên. Build profile có thể được lưu ở bất kỳ vị trí nào, nhưng bạn nên lưu ở đâu đó trong thư mục dự án và thêm vào version control để có thể quay lại sử dụng khi cần. Điều này cũng cho phép dùng version control để theo dõi các thay đổi đối với build profile.

Build profile là một tệp JSON (với phần mở rộng ``.gdbuild``) có dạng như sau sau khi phát hiện trong ví dụ trên:

::

    {
        "disabled_build_options": {
            "disable_navigation_3d": true,
            "disable_xr": true,
            "module_godot_physics_3d_enabled": false,
            "module_msdfgen_enabled": false,
            "module_openxr_enabled": false
        },
        "disabled_classes": [
            "AESContext",
            ...
            "ZIPReader"
        ],
        "type": "build_profile"
    }

Có thể truyền tệp này dưới dạng tùy chọn SCons khi :ref:`biên dịch <doc_compiling_index>` các export template:

::

    scons target=template_release build_profile=/path/to/profile.gdbuild

Buildsystem sẽ sử dụng tệp này để vô hiệu hóa các class không được sử dụng, nhờ đó giảm kích thước binary.

Các giới hạn
------------

Chức năng :button:`Detect from Project` dựa trên việc đọc các scene và script của dự án. Chức năng này sẽ không thể phát hiện các tính năng được sử dụng trong những trường hợp sau:

- Các tính năng được sử dụng trong những GDScript được tạo theo thủ tục rồi chạy tại runtime.
- Các tính năng được sử dụng trong :ref:`expression <doc_evaluating_expressions>`.
- Các tính năng được sử dụng trong :ref:`GDExtension <doc_gdextension>`, trừ khi language binding cho phép định nghĩa các class được sử dụng và extension sử dụng chức năng đó. Xem `GH-104129 <https://github.com/godotengine/godot/pull/104129>`__ để biết chi tiết.
- Các tính năng được sử dụng trong :ref:`PCK bên ngoài được tải tại runtime <doc_exporting_pcks>`.
- Có thể tồn tại một số trường hợp đặc biệt. Nếu không chắc chắn, vui lòng `mở issue trên GitHub <https://github.com/godotengine/godot/issues>`__ và đính kèm một dự án tái hiện tối giản.

.. seealso::

    Bạn có thể tiếp tục giảm kích thước bằng cách truyền các tùy chọn khác giúp giảm kích thước binary. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin.
