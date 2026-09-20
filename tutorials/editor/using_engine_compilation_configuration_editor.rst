.. _doc_engine_compilation_configuration_editor:

Sử dụng trình chỉnh sửa cấu hình biên dịch engine
=================================================

Godot đi kèm một tập hợp lớn các tính năng tích hợp sẵn. Mặc dù điều này rất tiện lợi, nhưng cũng có nghĩa là kích thước binary của Godot lớn hơn mức có thể, đặc biệt đối với các dự án chỉ sử dụng một phần nhỏ trong tập hợp tính năng này.

Để giúp giảm kích thước binary, bạn có thể biên dịch các export template tùy chỉnh với một số tính năng bị tắt. Nội dung này được mô tả chi tiết trong :ref:`doc_optimizing_for_size`. Tuy nhiên, việc xác định những tính năng nào cần tắt có thể khá tẻ nhạt. Trình chỉnh sửa cấu hình biên dịch engine giúp giải quyết vấn đề này bằng cách cung cấp một giao diện để dễ dàng xem và quản lý các tính năng, đồng thời có thể phát hiện những tính năng hiện đang được sử dụng trong dự án.

:menu:`Project > Tools > Engine Compilation Configuration Editor` cho phép bạn tạo và quản lý các build profile cho dự án Godot của mình.

Từ bây giờ, bạn có hai khả năng:

- Xem danh sách và bỏ chọn thủ công những tính năng bạn không cần. - Sử dụng nút :button:`Detect from Project` để tự động phát hiện các tính năng hiện đang được sử dụng trong dự án và tắt những tính năng không được sử dụng. Lưu ý rằng thao tác này sẽ ghi đè danh sách tính năng hiện tại, vì vậy nếu bạn đã bỏ chọn thủ công một số mục, trạng thái của chúng sẽ được đặt lại dựa trên việc dự án có thực sự sử dụng tính năng đó hay không.

.. figure:: img/engine_compilation_configuration_editor_detect.webp
   :align: center
   :alt: Opening the Engine Compilation Configuration Editor

   Opening the Engine Compilation Configuration Editor

Sau khi bạn nhấp vào :button:`Detect from Project`, bước phát hiện dự án sẽ bắt đầu. Quá trình này có thể mất từ vài giây đến vài phút, tùy thuộc vào kích thước dự án. Khi quá trình phát hiện hoàn tất, bạn sẽ thấy danh sách tính năng được cập nhật, trong đó một số tính năng đã bị tắt:

.. figure:: img/engine_compilation_configuration_editor_detected.webp
   :align: center
   :alt: Updated features list after using feature detection (example from the 3D platformer demo)

   Updated features list after using feature detection (example from the 3D platformer demo)

.. warning::

    Việc bỏ chọn các tính năng trong hộp thoại này sẽ không trực tiếp làm giảm kích thước binary khi export. Vì chỉ có thể thực sự loại bỏ các tính năng khỏi binary tại thời điểm biên dịch, bạn vẫn cần biên dịch các export template tùy chỉnh với build profile được chỉ định để thực sự hưởng lợi từ trình chỉnh sửa cấu hình biên dịch engine.

Bây giờ bạn có thể lưu build profile bằng cách nhấp vào **Save As** ở phía trên. Build profile có thể được lưu ở bất kỳ vị trí nào, nhưng bạn nên lưu ở đâu đó trong thư mục dự án và thêm vào version control để có thể quay lại sử dụng sau này khi cần. Điều này cũng cho phép dùng version control để theo dõi các thay đổi đối với build profile.

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

Có thể truyền tệp này dưới dạng tùy chọn SCons khi :ref:`compiling <doc_compiling_index>` export template:

::

    scons target=template_release build_profile=/path/to/profile.gdbuild

Buildsystem sẽ sử dụng thông tin này để tắt các class không được sử dụng và nhờ đó giảm kích thước binary.

Giới hạn
--------

Tính năng :button:`Detect from Project` dựa vào việc đọc các scene và script của dự án. Tính năng này sẽ không thể phát hiện các tính năng được sử dụng trong những trường hợp sau:

- Các tính năng được sử dụng trong GDScript được tạo theo cách thủ tục rồi chạy trong runtime. - Các tính năng được sử dụng trong :ref:`expressions <doc_evaluating_expressions>`. - Các tính năng được sử dụng trong :ref:`GDExtensions <doc_gdextension>`, trừ khi language binding cho phép xác định các class được sử dụng và extension sử dụng chức năng này. Xem `GH-104129 <https://github.com/godotengine/godot/pull/104129>`__ để biết chi tiết. - Các tính năng được sử dụng trong :ref:`external PCKs loaded at runtime <doc_exporting_pcks>`. - Có thể tồn tại một số trường hợp đặc biệt. Nếu không chắc chắn, vui lòng `open an issue on GitHub <https://github.com/godotengine/godot/issues>`__ và đính kèm một dự án tái hiện tối giản.

.. seealso::

    Bạn có thể tiếp tục giảm kích thước bằng cách truyền các tùy chọn khác giúp giảm kích thước binary. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin.
