.. _doc_ragdoll_system:

Hệ thống ragdoll
================

Giới thiệu
----------

Godot hỗ trợ vật lý ragdoll. Ragdoll dựa vào mô phỏng vật lý để tạo ra animation thủ tục chân thực. Chúng được sử dụng cho animation cái chết trong nhiều game.

Trong hướng dẫn này, chúng ta sẽ sử dụng bản demo Platformer 3D để thiết lập một ragdoll.

.. note::

    Bạn có thể tải bản demo Platformer 3D xuống tại `GitHub <https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer>`_ hoặc sử dụng `Asset Library <https://godotengine.org/asset-library/asset/2748>`_.

    Bạn cũng có thể xem ví dụ về một thiết lập ragdoll hoàn chỉnh trong `Ragdoll Physics demo <https://github.com/godotengine/godot-demo-projects/tree/master/3d/ragdoll_physics>`_.

Thiết lập ragdoll
-----------------

Tạo các xương vật lý
~~~~~~~~~~~~~~~~~~~~

Giống như nhiều tính năng khác trong engine, có hai node được sử dụng để thiết lập ragdoll:

- Một node :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>`. Node này là parent của tất cả các xương vật lý và chịu trách nhiệm điều khiển mô phỏng. - Một hoặc nhiều node con :ref:`PhysicalBone3D <class_PhysicalBone3D>`. Mỗi node đại diện cho một xương riêng lẻ trong ragdoll.

Mở bản demo platformer trong Godot, sau đó mở scene ``player/player.tscn``. Chọn node ``Skeleton3D``. Một nút skeleton sẽ xuất hiện ở đầu viewport của trình chỉnh sửa 3D:

.. figure:: img/ragdoll_system_create_physical_skeleton.webp
   :align: center
   :alt: Creating a physical skeleton in the editor

   Creating a physical skeleton in the editor

Nhấp vào đó và chọn tùy chọn :menu:`Create Physical Skeleton`. Godot sẽ tạo các node PhysicalBone3D và các shape va chạm cho mỗi xương trong skeleton, cùng các khớp pin để kết nối chúng với nhau:

.. figure:: img/ragdoll_system_skeleton_scene_tree.webp
   :align: center
   :alt: Scene tree of the player scene after creating a physical skeleton

   Scene tree of the player scene after creating a physical skeleton

Một số xương được tạo không cần thiết, chẳng hạn như xương ``MASTER`` trong scene này. Chúng ta sẽ dọn dẹp skeleton bằng cách xóa chúng.

Dọn dẹp và tối ưu skeleton
~~~~~~~~~~~~~~~~~~~~~~~~~~

Mỗi PhysicalBone3D mà engine cần mô phỏng đều gây ra một chi phí hiệu năng. Bạn nên xóa mọi xương quá nhỏ để tạo ra khác biệt trong mô phỏng, cũng như tất cả các xương tiện ích.

Ví dụ, với một nhân vật hình người, bạn không cần có xương vật lý cho từng ngón tay. Thay vào đó, bạn có thể dùng một xương duy nhất cho toàn bộ bàn tay, hoặc một xương cho lòng bàn tay, một xương cho ngón cái và một xương cuối cho bốn ngón tay còn lại.

Xóa các node PhysicalBone3D này: ``MASTER``, ``waist``, ``neck``, ``headtracker``. Điều này tạo ra một skeleton được tối ưu và giúp điều khiển ragdoll dễ dàng hơn.

Điều chỉnh các khớp và ràng buộc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi điều chỉnh các shape va chạm, ragdoll của bạn gần như đã sẵn sàng. Bây giờ, bạn cần điều chỉnh các khớp pin để có mô phỏng tốt hơn. Theo mặc định, các node PhysicalBone3D được gán một khớp pin không có ràng buộc. Để thay đổi khớp pin, hãy chọn một node PhysicalBone3D và thay đổi loại ràng buộc trong phần :menu:`Joint` của inspector. Tại đó, bạn có thể thay đổi hướng và các giới hạn của ràng buộc.

Các khớp cũng có gizmo hiển thị trong trình chỉnh sửa 3D, vì vậy bạn có thể thấy các ràng buộc của chúng hoạt động.

.. figure:: img/ragdoll_system_adjust_joints_inspector.webp
   :align: center
   :alt: Adjusting joints in the inspector after selecting a PhysicalBone3D node

   Adjusting joints in the inspector after selecting a PhysicalBone3D node

.. tip::

    Để có góc nhìn tốt hơn khi chỉnh sửa các khớp và shape va chạm, bạn có thể làm như sau:

    - Hide PhysicalBone3D nodes you aren't currently working on, so you can focus on the ones you're adjusting. - Hide the MeshInstance3D of the character by clicking the eye icon next to it in the scene tree dock. - Hide the Skeleton3D gizmos, so that the orange triangles that represent the skeleton don't clutter the viewport while leaving the rest visible. To do so, click :menu:`View > Gizmos > Skeleton3D` at the top of the 3D editor viewport until the eye icon appears closed. - Disable the preview environment by clicking the globe icon at the top of the 3D editor viewport. - Set the **Default Clear Color** project setting to pure black in the Project Settings. This is only effective if the preview environment is disabled. - Change the debug draw mode using the :menu:`Perspective` button in the top-left corner of the 3D editor viewport. The :menu:`Display Wireframe` and :menu:`Display Overdraw` options are particularly useful when adjusting collision shapes, as they allow you to see through the original mesh. - Use the orthographic camera by clicking the :button:`X`/:button:`Y`/:button:`Z` buttons in the top-right corner of the 3D editor viewport.

Dưới đây là danh sách các khớp hiện có:

- **None:** Không áp dụng bất kỳ ràng buộc nào. - **ConeJoint:** Ball-and-socket. Hữu ích cho vai, hông và cổ. - **HingeJoint:** Cung cấp ràng buộc góc; hãy hình dung nó như bản lề cửa. Hữu ích cho khuỷu tay và đầu gối. - **PinJoint:** Giữ hai body được kết nối *(mặc định)*. Khiến các xương bị “co dúm”, vì vậy bạn nên sử dụng các loại khớp khác cho hầu hết nhân vật. - **SliderJoint:** Trượt một xương dọc theo xương khác trên một trục cụ thể. - **6DOFJoint:** Khớp mạnh mẽ nhất, cung cấp cả ràng buộc tuyến tính và góc, nhưng cũng là khớp phức tạp nhất để cấu hình.

Nếu không chắc chắn, hãy bắt đầu với HingeJoint và ConeJoint, vì chúng đáp ứng hầu hết trường hợp sử dụng:

- Đối với HingeJoint, hãy đảm bảo bật **Angular Limit** trong
  :menu:`Joint Constraints` section of the inspector. After enabling it,
  bạn có thể thấy góc mà nó bị giới hạn trong viewport. Bạn có thể xoay PhysicalBone3D để thay đổi trục mà khớp bị giới hạn, sau đó điều chỉnh các góc. - Đối với ConeJoint, thông thường tốt nhất là giới hạn **Swing Span** trong khoảng từ 20 đến 90 độ, và **Twist Span** trong khoảng từ 20 đến 45 độ.

Điều chỉnh các shape va chạm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nhiệm vụ tiếp theo là điều chỉnh shape va chạm và kích thước của các xương vật lý để khớp với phần cơ thể mà mỗi xương cần mô phỏng.

Bạn nên điều chỉnh các shape va chạm *sau khi* điều chỉnh các khớp và ràng buộc, vì việc xoay một khớp cũng sẽ xoay shape va chạm. Để tránh phải điều chỉnh các shape va chạm hai lần, tốt hơn hết là điều chỉnh các khớp trước.

Lưu ý rằng một node PhysicalBone3D có thể có nhiều shape va chạm làm node con. Điều này hữu ích để biểu diễn các hình dạng đặc biệt phức tạp của các chi vốn cứng.

.. tip::

    Để tạm dừng việc phát animation trong khi điều chỉnh ragdoll, hãy chọn node ``AnimationTree`` và tắt thuộc tính **Active** trong Inspector. Hãy nhớ bật lại thuộc tính này khi hoàn tất, vì nó điều khiển việc phát animation trong quá trình gameplay.

.. figure:: img/ragdoll_system_adjust_collision_shapes.webp
   :align: center
   :alt: Adjusting collision shapes in the 3D editor

   Adjusting collision shapes in the 3D editor

Đây là kết quả cuối cùng:

.. figure:: img/ragdoll_system_result.webp
   :align: center
   :alt: Result after adjusting joints and collision shapes (player mesh is hidden for visibility)

   Result after adjusting joints and collision shapes (player mesh is hidden for visibility)

Mô phỏng ragdoll
----------------

Ragdoll hiện đã sẵn sàng để sử dụng. Để bắt đầu mô phỏng và phát animation ragdoll, bạn cần gọi
:ref:`PhysicalBoneSimulator3D.physical_bones_start_simulation() <class_PhysicalBoneSimulator3D_method_physical_bones_start_simulation>`
method. Gắn một script vào node :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>`, là parent của tất cả các node PhysicalBone3D trong scene của chúng ta, sau đó gọi nó trong method ``_ready`` của script:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        physical_bones_start_simulation()

 .. code-tab:: csharp

    public override void _Ready()
    {
        PhysicalBonesStartSimulation();
    }

Để dừng mô phỏng, hãy gọi
:ref:`PhysicalBoneSimulator3D.physical_bones_stop_simulation() <class_PhysicalBoneSimulator3D_method_physical_bones_stop_simulation>`
method.

.. video:: video/ragdoll_system_full_simulation.webm
    :alt: Full simulation of ragdoll system, with the player falling to the ground
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

Bạn cũng có thể giới hạn mô phỏng chỉ ở một vài xương. Điều này hữu ích để tạo các hiệu ứng như chi ragdoll hoặc các phần gắn thêm có thể tương tác với thế giới. Để làm vậy, hãy truyền tên xương (*không phải* tên node PhysicalBone3D) làm tham số. Để xem tên xương, hãy xem thuộc tính **Bone Name** trong inspector sau khi chọn một node PhysicalBone3D.

.. tip::

    Khi sử dụng skeleton vật lý được tạo tự động như trong hướng dẫn này, tên xương cũng nằm trong tên node. Ví dụ, trong ``Physical Bone l-arm``, ``l-arm`` là tên xương.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        physical_bones_start_simulation(["l-arm", "r-arm"])

 .. code-tab:: csharp

    public override void _Ready()
    {
        PhysicalBonesStartSimulation(["l-arm", "r-arm"]);
    }

Lưu ý rằng các tên xương không tồn tại sẽ không in ra bất kỳ lỗi hoặc cảnh báo nào. Nếu không có gì xảy ra khi bắt đầu mô phỏng (hoặc nếu toàn bộ cơ thể bị ragdoll thay vì chỉ các xương cụ thể), hãy kiểm tra lại danh sách các xương đã cung cấp.

Dưới đây là một ví dụ về mô phỏng ragdoll một phần:

.. video:: video/ragdoll_system_partial_simulation.webm
    :alt: Partial simulation of ragdoll system, with arms flailing while the player is walking
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tip::

    Để kiểm soát mức độ ảnh hưởng của mô phỏng ragdoll một phần lên animation tổng thể, bạn có thể điều chỉnh thuộc tính **Influence** trong
    :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>` node that is the
    parent của tất cả các node PhysicalBone3D. Theo mặc định, thuộc tính này được đặt thành ``1.0``, nghĩa là mô phỏng ragdoll sẽ hoàn toàn ghi đè phần animation còn lại.

Layer và mask va chạm
~~~~~~~~~~~~~~~~~~~~~

Hãy đảm bảo thiết lập đúng các layer và mask va chạm để capsule của CharacterBody3D không cản trở mô phỏng vật lý. Đồng thời nhớ điều chỉnh layer và mask va chạm trong scene coin để người chơi vẫn có thể nhặt coin:

.. figure:: img/ragdoll_system_collision_layers_masks.webp
   :align: center
   :alt: Layers and masks must be adjusted to these values in the inspector for each node

   Layers and masks must be adjusted to these values in the inspector for each node

Bạn có thể tìm thấy GridMap trong bản demo platformer 3D tại ``stage/grid_map.scn``. Node Area3D của coin (nơi cần điều chỉnh các layer và mask) có thể được tìm thấy tại ``coin/coin.tscn``.

.. tip::

    Để nhanh chóng chọn tất cả các node PhysicalBone3D, hãy nhập ``t:PhysicalBone3D`` vào thanh tìm kiếm ở đầu dock cây scene. Thao tác này sẽ lọc cây scene để chỉ hiển thị các node PhysicalBone3D, cho phép bạn chọn tất cả cùng lúc bằng :kbd:`Shift + Left mouse button` trên mục đầu tiên và mục cuối cùng.

Nếu không thực hiện việc này, va chạm sẽ hoạt động không chính xác vì người chơi sẽ va chạm với ragdoll (không hoạt động) của chính mình. Điều này có thể khiến người chơi bật nảy dữ dội hoặc bị kẹt.

Giống như RigidBody3D, PhysicalBone3D hỗ trợ các ngoại lệ va chạm thông qua code bằng cách sử dụng các method :ref:`physical_bones_add_collision_exception() <class_PhysicalBoneSimulator3D_method_physical_bones_add_collision_exception>` và :ref:`physical_bones_remove_collision_exception() <class_PhysicalBoneSimulator3D_method_physical_bones_remove_collision_exception>`. Bạn có thể dùng cách này để ngăn va chạm với một object cụ thể mà không cần dựa vào layer và mask.

.. seealso::

    Để biết thêm thông tin, hãy xem :ref:`doc_physics_introduction_collision_layers_and_masks`.
