.. _doc_openxr_render_models:

Mô hình kết xuất OpenXR
=======================

Một nguyên tắc cốt lõi trong thiết kế API của OpenXR là không phụ thuộc vào nền tảng nhiều nhất có thể. Một ví dụ điển hình là hệ thống action map của OpenXR, trong đó các XR runtime phải hỗ trợ những interaction profile cốt lõi để dùng làm phương án dự phòng nếu không tồn tại interaction profile cho phần cứng đang sử dụng. Điều này đảm bảo các ứng dụng OpenXR vẫn tiếp tục hoạt động ngay cả khi được sử dụng trên phần cứng chưa tồn tại vào thời điểm ứng dụng được phát hành, hoặc mà các nhà phát triển ứng dụng không có quyền tiếp cận.

Một hệ quả của điều này là nhà phát triển ứng dụng không biết chắc phần cứng nào đang được sử dụng, vì XR runtime có thể mô phỏng phần cứng khác. Do đó, nhà phát triển ứng dụng không thể hiển thị bất kỳ nội dung nào liên quan đến phần cứng thực tế đang được sử dụng; trường hợp phổ biến nhất là hiển thị các tay cầm mà người dùng hiện đang cầm.

Việc hiển thị đúng các mô hình tay cầm và định vị chính xác các mô hình này rất quan trọng để tạo cảm giác đắm chìm phù hợp.

Đây là lúc `API render models <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_render_models>`_ của OpenXR phát huy tác dụng. API này cho phép chúng ta truy vấn XR runtime để lấy các tài sản 3D phù hợp với phần cứng vật lý đang được sử dụng. API cũng cho phép chúng ta truy vấn vị trí của phần cứng này trong vùng tracking và vị trí chính xác của các thành phần con của phần cứng.

Ví dụ, chúng ta có thể định vị và tạo animation chính xác cho cò, hoặc hiển thị các nút đang được nhấn.

Đối với những runtime hỗ trợ `controller data source for hand tracking <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking_data_source>`_ , chúng ta cũng có thể định vị chính xác các ngón tay và bàn tay của người dùng theo hình dạng của tay cầm. Lưu ý rằng tính năng này hoạt động kết hợp với `hand joints motion range extension <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_joints_motion_range>`_ để ngăn các ngón tay bị xuyên vào vật thể.

Node OpenXR Render models
-------------------------

:ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` node có thể được sử dụng để tự động hóa hầu hết chức năng render models. Node này theo dõi các render models đang hoạt động hiện được XR runtime cung cấp.

Node này sẽ tạo các node con cho mỗi render model đang hoạt động, nhờ đó render model đó được hiển thị.

Node này phải có một :ref:`XROrigin3D<class_XROrigin3D>` node làm tổ tiên.

Nếu ``tracker`` được đặt thành ``Any`` thì node của chúng ta sẽ hiển thị tất cả render models hiện đang được tracking. Trong trường hợp này, node này phải là node con trực tiếp của :ref:`XROrigin3D<class_XROrigin3D>` node.

Nếu ``tracker`` được đặt thành ``None set`` thì node của chúng ta sẽ chỉ hiển thị các render models chưa xác định được tracker nào. Trong trường hợp này, node này cũng phải là node con trực tiếp của
:ref:`XROrigin3D<class_XROrigin3D>` node.

Nếu ``tracker`` được đặt thành ``Left Hand`` hoặc ``Right Hand`` thì node của chúng ta sẽ chỉ hiển thị các render models tương ứng với tay trái hoặc tay phải. Trong trường hợp này, node của chúng ta có thể được đặt sâu hơn trong scene tree.

.. warning::

    Đối với hầu hết XR runtime, điều này có nghĩa là render model đại diện cho một tay cầm thực sự đang được người dùng cầm, nhưng đây không phải là điều được đảm bảo. Một số XR runtime sẽ luôn đặt tracker thành tay trái hoặc tay phải, ngay cả khi tay cầm hiện không được cầm nhưng vẫn đang được tracking. Bạn luôn nên kiểm tra điều này, vì nó sẽ dẫn đến hành vi không mong muốn.

Trong trường hợp này, chúng ta cũng có thể chỉ định một action cho một pose trong action map bằng cách đặt thuộc tính ``make_local_to_pose`` thành pose action. Kết hợp với một :ref:`XRController3D<class_XRController3D>` node đang sử dụng cùng pose, giờ đây bạn có thể thêm một lớp cho phép lệch khỏi vị trí được tracking của cả tay cầm và render model liên quan (xem ví dụ bên dưới).

.. note::

    Việc kết hợp nội dung trên với hand tracking làm phát sinh vấn đề là hand tracking hoàn toàn độc lập với hệ thống action map. Bạn sẽ cần kết hợp các pose tracking của bàn tay và tay cầm để offset render models một cách chính xác.

    Nội dung này nằm ngoài phạm vi của tài liệu.

Ví dụ về render model manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể tải xuống `bản demo render models của chúng tôi <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_render_models>`_, trong đó triển khai thiết lập được mô tả bên dưới.

.. image:: img/openxr_render_models_setup.webp

Trong thiết lập này, chúng ta tìm thấy một :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` node nằm ngay bên dưới :ref:`XROrigin3D<class_XROrigin3D>` node. Trên node này, thuộc tính ``target`` được đặt thành ``None set`` và sẽ xử lý việc hiển thị tất cả render models hiện không liên quan đến tay cầm bên trái hoặc bên phải của chúng ta.

Sau đó, chúng ta thấy thiết lập tương tự cho tay trái và tay phải, vì vậy chúng ta sẽ chỉ tập trung vào tay trái.

Chúng ta có một :ref:`XRController3D<class_XRController3D>` để tracking vị trí bàn tay.

.. note::

    Trong ví dụ này, chúng ta sử dụng pose ``grip``. Tuy nhiên, pose ``palm`` được cho là phù hợp và dễ dự đoán hơn, nhưng không được tất cả XR runtime hỗ trợ. Hãy xem dự án hand tracking demo để biết giải pháp chuyển đổi giữa các pose này dựa trên những gì được hỗ trợ.

Là node con của node này, chúng ta có một :ref:`AnimatableBody3D<class_AnimatableBody3D>` node đi theo vị trí được tracking của bàn tay **nhưng** sẽ tương tác với các physics object để ngăn bàn tay của người chơi đi xuyên qua tường, v.v. Node này có một collision shape bao quanh bàn tay.

.. note::

    Điều quan trọng là phải đặt physics priority để logic này chạy sau mọi physics logic di chuyển XROrigin3D node; nếu không, bàn tay sẽ bị trễ một frame.

Script bên dưới cho thấy một triển khai cơ bản mà bạn có thể phát triển thêm.

.. code-block:: gdscript

    class_name CollisionHands3D
    extends AnimatableBody3D

    func _ready():
        # Đảm bảo các giá trị này được thiết lập chính xác.
        top_level = true
        sync_to_physics = false
        process_physics_priority = -90

    func _physics_process(_delta):
        # Đi theo parent node của chúng ta.
        var dest_transform = get_parent().global_transform

        # Trong ví dụ này, chúng ta chỉ áp dụng rotation.
        global_basis = dest_transform.basis

        # Cố gắng di chuyển đến vị trí bàn tay đang được tracking.
        move_and_collide(dest_transform.origin - global_position)


Cuối cùng, chúng ta thấy một :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` node khác, node này có ``target`` được đặt thành bàn tay tương ứng và ``make_local_to_pose`` được đặt thành pose chính xác. Điều này đảm bảo các render models liên quan đến bàn tay này được hiển thị chính xác và offset nếu collision handler đã thay đổi vị trí.

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/_gNOd7wQ62M" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>


Node render model
-----------------

:ref:`OpenXRRenderModel<class_OpenXRRenderModel>` node triển khai toàn bộ logic để hiển thị và định vị một render model cụ thể do render models API cung cấp.

Các instance của node này được thêm bởi render model manager node mà chúng ta đã sử dụng ở trên, nhưng nếu muốn, bạn có thể tương tác trực tiếp với chúng.

Mỗi khi Godot nhận được thông tin về một render model mới, một RID sẽ được tạo để tham chiếu đến render model đó.

Bằng cách gán RID đó cho thuộc tính ``render_model`` trên node này, node sẽ bắt đầu hiển thị render model và quản lý cả transform đặt render model vào đúng vị trí lẫn việc tạo animation cho tất cả object con.

Hàm ``get_top_level_path`` sẽ trả về path cấp cao nhất được liên kết với render model này. Path này sẽ trỏ đến tay trái hoặc tay phải. Vì path cấp cao nhất có thể được thiết lập hoặc xóa tùy thuộc vào việc người dùng nhấc hoặc đặt controller xuống, bạn có thể kết nối với signal ``render_model_top_level_path_changes`` và phản hồi các thay đổi này.

Tùy thuộc vào thiết lập của
:ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` node, các render model sẽ bị xóa hoặc thêm vào khi path cấp cao nhất của chúng thay đổi.

Truy cập backend
----------------

Các node được trình bày chi tiết ở trên xử lý toàn bộ logic hiển thị cho chúng ta, nhưng bạn cũng có thể tương tác trực tiếp với dữ liệu điều khiển logic này và tạo implementation của riêng mình.

Để thực hiện việc này, bạn có thể truy cập
singleton :ref:`OpenXRRenderModelExtension<class_OpenXRRenderModelExtension>`.

Đối tượng này cũng cho phép bạn truy vấn xem render model có được thiết bị hiện đang sử dụng hỗ trợ và bật hay không bằng cách gọi hàm ``is_active`` trên đối tượng này.

Logic tích hợp sẵn triển khai API `interaction render model API <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_interaction_render_model>`_, trong đó liệt kê tất cả render model liên quan đến controller và các thiết bị tương tự hiện diện trong action map. Logic này sẽ tự động tạo và xóa các thực thể render model được cung cấp qua API này.

Khi có các extension khác, bạn có thể triển khai chúng trong một plugin GDExtension. Plugin như vậy có thể gọi ``render_model_create`` và ``render_model_destroy`` để tạo đối tượng cung cấp quyền truy cập vào render model đó thông qua core render models API.

Bạn không nên hủy render model bên ngoài logic này.

Bạn có thể kết nối với các signal ``render_model_added`` và ``render_model_removed`` để được thông báo khi render model mới được thêm vào hoặc bị xóa.

Các phương thức cốt lõi để làm việc với API này được liệt kê bên dưới:

.. list-table:: Các hàm mở rộng render model
   :header-rows: 1

   * - Hàm
     - Mô tả
   * - render_model_get_all
     - Cung cấp một mảng RID cho tất cả render model đang được theo dõi.
   * - render_model_new_scene_instance
     - Cung cấp một scene mới chứa tất cả mesh cần thiết để hiển thị render model.
   * - render_model_get_subaction_paths
     - Cung cấp danh sách subaction path từ action map của bạn liên quan đến render model này.
   * - render_model_get_top_level_path
     - Trả về path cấp cao nhất được liên kết với render model này (nếu có). Sử dụng signal ``render_model_top_level_path_changed`` để phản hồi khi giá trị này thay đổi.
   * - render_model_get_confidence
     - Trả về độ tin cậy theo dõi của dữ liệu theo dõi cho render model này.
   * - render_model_get_root_transform
     - Trả về root transform của render model này trong reference space hiện tại của chúng ta. Bạn có thể sử dụng giá trị này để đặt render model trong không gian.
   * - render_model_get_animatable_node_count
     - Trả về số node trong scene render model của chúng ta có thể được animate
   * - render_model_get_animatable_node_name
     - Trả về tên của node mà chúng ta có thể animate. Lưu ý rằng node này có thể nằm ở bất kỳ độ sâu nào trong scene.
   * - render_model_is_animatable_node_visible
     - Trả về true nếu animatable node này cần được hiển thị
   * - render_model_get_animatable_node_transform
     - Trả về transform của animatable node này. Đây là local transform có thể được áp dụng trực tiếp.

.. _`render models API`: https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_render_models
.. _`controller data source for hand tracking`: https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking_data_source
.. _`hand joints motion range extension`: https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_joints_motion_range
.. _`our render models demo`: https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_render_models
.. _`interaction render model API`: https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_interaction_render_model
