.. _doc_openxr_render_models:

Render Models của OpenXR
========================

Một nền tảng cốt lõi trong thiết kế API của OpenXR là tính độc lập với nền tảng cao nhất có thể. Một ví dụ điển hình là hệ thống action map của OpenXR, trong đó các XR runtime phải hỗ trợ những interaction profile cốt lõi để dự phòng nếu không tồn tại interaction profile cho phần cứng đang được sử dụng. Điều này đảm bảo các ứng dụng OpenXR vẫn tiếp tục hoạt động ngay cả khi được sử dụng trên phần cứng chưa tồn tại tại thời điểm ứng dụng được phát hành, hoặc mà các nhà phát triển ứng dụng không có quyền tiếp cận.

Hệ quả của điều này là nhà phát triển ứng dụng không thể biết chắc phần cứng nào đang được sử dụng, vì XR runtime có thể mô phỏng phần cứng khác. Do đó, nhà phát triển ứng dụng không thể hiển thị bất cứ thứ gì liên quan đến phần cứng thực tế đang được sử dụng; trường hợp phổ biến nhất là hiển thị các controller mà người dùng hiện đang cầm.

Việc hiển thị đúng các model controller và định vị chính xác các model này rất quan trọng để tạo cảm giác hòa mình phù hợp.

Đây là lúc `render models API <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_render_models>`_ của OpenXR phát huy tác dụng. API này cho phép chúng ta truy vấn XR runtime để lấy các tài sản 3D phù hợp với phần cứng vật lý đang được sử dụng. API cũng cho phép chúng ta truy vấn vị trí của phần cứng này trong tracking volume và vị trí chính xác của các thành phần con của phần cứng.

Ví dụ, chúng ta có thể định vị và tạo animation chính xác cho trigger hoặc hiển thị các nút đang được nhấn.

Đối với các runtime hỗ trợ `controller data source for hand tracking <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking_data_source>`_, chúng ta cũng có thể định vị chính xác các ngón tay và bàn tay của người dùng theo hình dạng của controller. Lưu ý rằng tính năng này hoạt động kết hợp với `hand joints motion range extension <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_joints_motion_range>`_ để tránh các ngón tay bị xuyên qua vật thể.

Node OpenXR Render models
-------------------------

Node :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` có thể được dùng để tự động hóa hầu hết chức năng render models. Node này theo dõi các render model đang hoạt động hiện được XR runtime cung cấp.

Node này sẽ tạo các node con cho từng render model đang hoạt động, khiến render model đó được hiển thị.

Node này phải có một node :ref:`XROrigin3D<class_XROrigin3D>` làm ancestor.

Nếu ``tracker`` được đặt thành ``Any``, node của chúng ta sẽ hiển thị tất cả render model hiện đang được tracking. Trong trường hợp này, node này phải là node con trực tiếp của node :ref:`XROrigin3D<class_XROrigin3D>`.

Nếu ``tracker`` được đặt thành ``None set``, node của chúng ta sẽ chỉ hiển thị các render model chưa xác định được tracker. Trong trường hợp này, node này cũng phải là node con trực tiếp của
:ref:`XROrigin3D<class_XROrigin3D>` node.

Nếu ``tracker`` được đặt thành ``Left Hand`` hoặc ``Right Hand``, node của chúng ta sẽ chỉ hiển thị các render model tương ứng với tay trái hoặc tay phải. Trong trường hợp này, node của chúng ta có thể được đặt sâu hơn trong scene tree.

.. warning::

    Đối với hầu hết XR runtime, điều này có nghĩa là render model đại diện cho một controller thực sự đang được người dùng cầm, nhưng đây không phải là điều được đảm bảo. Một số XR runtime sẽ luôn đặt tracker thành tay trái hoặc tay phải, ngay cả khi controller hiện không được cầm nhưng vẫn đang được tracking. Bạn luôn nên kiểm thử điều này vì nó có thể dẫn đến hành vi không mong muốn.

Trong trường hợp này, chúng ta cũng có thể chỉ định một action cho pose trong action map bằng cách đặt thuộc tính ``make_local_to_pose`` thành pose action. Kết hợp thuộc tính này với một node :ref:`XRController3D<class_XRController3D>` đang sử dụng cùng pose, giờ đây bạn có thể thêm một layer cho phép thay đổi vị trí tracking của cả controller và render model liên quan (xem ví dụ bên dưới).

.. note::

    Việc kết hợp nội dung trên với hand tracking tạo ra một vấn đề: hand tracking hoàn toàn độc lập với hệ thống action map. Bạn sẽ cần kết hợp các pose hand tracking và controller tracking để offset render model đúng cách.

    Điều này nằm ngoài phạm vi của tài liệu này.

Ví dụ về render model manager
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể tải xuống `our render models demo <https://github.com/godotengine/godot-demo-projects/tree/master/xr/openxr_render_models>`_, trong đó triển khai thiết lập được mô tả bên dưới.

.. image:: img/openxr_render_models_setup.webp

Trong thiết lập này, chúng ta tìm thấy một node :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` nằm ngay bên dưới node :ref:`XROrigin3D<class_XROrigin3D>`. Trên node này, thuộc tính ``target`` được đặt thành ``None set`` và sẽ xử lý việc hiển thị tất cả render model hiện không liên quan đến controller tay trái hoặc tay phải của chúng ta.

Sau đó, chúng ta thấy cùng một thiết lập cho tay trái và tay phải, vì vậy chúng ta sẽ chỉ tập trung vào tay trái.

Chúng ta có một :ref:`XRController3D<class_XRController3D>` để tracking vị trí bàn tay.

.. note::

    Trong ví dụ này, chúng ta sử dụng pose ``grip``. Pose ``palm`` được cho là phù hợp và dễ dự đoán hơn, tuy nhiên không được tất cả XR runtime hỗ trợ. Hãy xem project hand tracking demo để biết giải pháp chuyển đổi giữa các pose này dựa trên những pose được hỗ trợ.

Là node con của node này, chúng ta có một node :ref:`AnimatableBody3D<class_AnimatableBody3D>` đi theo vị trí tracking của bàn tay **nhưng** sẽ tương tác với các physics object để ngăn bàn tay của người chơi đi xuyên qua tường, v.v. Node này có một collision shape bao quanh bàn tay.

.. note::

    Điều quan trọng là phải đặt physics priority để logic này chạy sau mọi physics logic di chuyển node XROrigin3D; nếu không, bàn tay sẽ bị trễ một frame.

Script bên dưới cho thấy một cách triển khai cơ bản mà bạn có thể xây dựng thêm.

.. code-block:: gdscript

    class_name CollisionHands3D
    extends AnimatableBody3D

    func _ready():
        # Hãy đảm bảo các giá trị này được thiết lập chính xác.
        top_level = true
        sync_to_physics = false
        process_physics_priority = -90

    func _physics_process(_delta):
        # Đi theo node cha của chúng ta.
        var dest_transform = get_parent().global_transform

        # Trong ví dụ này, chúng ta chỉ áp dụng rotation.
        global_basis = dest_transform.basis

        # Cố gắng di chuyển đến vị trí bàn tay đang được tracking.
        move_and_collide(dest_transform.origin - global_position)


Cuối cùng, chúng ta thấy một node :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` khác; node này có ``target`` được đặt thành bàn tay tương ứng và ``make_local_to_pose`` được đặt thành pose chính xác. Điều này đảm bảo các render model liên quan đến bàn tay này được hiển thị đúng và offset nếu collision handler đã thay đổi vị trí.

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/_gNOd7wQ62M" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>


Node render model
-----------------

Node :ref:`OpenXRRenderModel<class_OpenXRRenderModel>` triển khai toàn bộ logic để hiển thị và định vị một render model cụ thể do render models API cung cấp.

Các instance của node này được thêm bởi render model manager node mà chúng ta đã sử dụng ở trên, nhưng bạn cũng có thể tương tác trực tiếp với chúng nếu muốn.

Mỗi khi Godot nhận được thông tin về một render model mới, một RID sẽ được tạo để tham chiếu đến render model đó.

Bằng cách gán RID đó cho thuộc tính ``render_model`` trên node này, node sẽ bắt đầu hiển thị render model và quản lý cả transform đặt render model vào đúng vị trí lẫn việc tạo animation cho tất cả object con.

Hàm ``get_top_level_path`` sẽ trả về top level path liên kết với render model này. Path này sẽ trỏ đến tay trái hoặc tay phải. Vì top level path có thể được thiết lập hoặc xóa tùy thuộc vào việc người dùng cầm lên hay đặt controller xuống, bạn có thể kết nối với signal ``render_model_top_level_path_changes`` và phản ứng với những thay đổi này.

Tùy thuộc vào thiết lập của
:ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>` nodes,
các render model sẽ bị xóa hoặc được thêm vào khi top level path của chúng thay đổi.

Truy cập backend
----------------

Các node được mô tả chi tiết ở trên xử lý toàn bộ logic hiển thị cho chúng ta, nhưng bạn vẫn có thể tương tác trực tiếp với dữ liệu điều khiển chúng và tạo triển khai của riêng mình.

Để làm vậy, bạn có thể truy cập
:ref:`OpenXRRenderModelExtension<class_OpenXRRenderModelExtension>`
singleton.

Object này cũng cho phép bạn truy vấn xem render model có được hỗ trợ và bật trên thiết bị hiện đang được sử dụng hay không bằng cách gọi hàm ``is_active`` trên object này.

Logic tích hợp sẵn triển khai `interaction render model API <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_interaction_render_model>`_, liệt kê tất cả render model liên quan đến controller và các thiết bị tương tự hiện diện trong action map. Logic này sẽ tự động tạo và xóa các entity render model được cung cấp thông qua API này.

Khi có các extension khác, chúng có thể được triển khai trong một plugin GDExtension. Plugin như vậy có thể gọi ``render_model_create`` và ``render_model_destroy`` để tạo object cung cấp quyền truy cập vào render model đó thông qua core render models API.

Bạn không nên hủy một render model bên ngoài logic này.

Bạn có thể kết nối với các signal ``render_model_added`` và ``render_model_removed`` để được thông báo khi render model mới được thêm vào hoặc xóa đi.

Các phương thức cốt lõi để làm việc với API này được liệt kê bên dưới:

.. list-table:: Render model extension functions
   :header-rows: 1

   * - Hàm
     - Mô tả
   * - render_model_get_all
     - Cung cấp một mảng RID cho tất cả render model
       đang được tracking.
   * - render_model_new_scene_instance
     - Cung cấp một scene mới chứa tất cả mesh
       cần thiết để hiển thị render model.
   * - render_model_get_subaction_paths
     - Cung cấp danh sách subaction path từ
       action map liên quan đến render model này.
   * - render_model_get_top_level_path
     - Trả về top level path liên kết với
       render model này (nếu có).
       Sử dụng signal ``render_model_top_level_path_changed``
       để phản ứng với thay đổi này.
   * - render_model_get_confidence
     - Trả về độ tin cậy tracking của dữ liệu
       tracking cho render model này.
   * - render_model_get_root_transform
     - Trả về root transform của render model này
       trong reference space hiện tại của chúng ta. Giá trị này có thể được
       dùng để đặt render model trong không gian.
   * - render_model_get_animatable_node_count
     - Trả về số node trong scene render model của chúng ta
       có thể được tạo animation
   * - render_model_get_animatable_node_name
     - Trả về tên của node mà chúng ta có thể animate.
       Lưu ý rằng node này có thể nằm ở bất kỳ số cấp độ nào
       bên trong scene.
   * - render_model_is_animatable_node_visible
     - Trả về true nếu node có thể animate này cần được
       hiển thị
   * - render_model_get_animatable_node_transform
     - Trả về transform của node có thể animate này.
       Đây là một local transform có thể được
       áp dụng trực tiếp.


