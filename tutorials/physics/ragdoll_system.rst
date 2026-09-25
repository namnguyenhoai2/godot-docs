.. _doc_ragdoll_system:

Hệ thống ragdoll
================

Giới thiệu
----------

Godot hỗ trợ vật lý ragdoll. Ragdoll dựa vào mô phỏng vật lý để tạo ra hoạt ảnh thủ tục chân thực. Chúng được sử dụng cho hoạt ảnh nhân vật chết trong nhiều trò chơi.

Trong hướng dẫn này, chúng ta sẽ sử dụng bản demo Platformer 3D để thiết lập một ragdoll.

.. note::

    Bạn có thể tải bản demo Platformer 3D xuống từ `GitHub <https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer>`_ hoặc sử dụng `Asset Library <https://godotengine.org/asset-library/asset/2748>`_.

    Bạn cũng có thể xem một ví dụ về thiết lập ragdoll hoàn chỉnh trong `Ragdoll Physics demo <https://github.com/godotengine/godot-demo-projects/tree/master/3d/ragdoll_physics>`_.

Thiết lập ragdoll
-----------------

Tạo các xương vật lý
~~~~~~~~~~~~~~~~~~~~

Giống như nhiều tính năng khác trong engine, có hai node được sử dụng để thiết lập ragdoll:

- Một node :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>`. Node này là node cha của tất cả các xương vật lý và chịu trách nhiệm điều khiển mô phỏng.
- Một hoặc nhiều node con :ref:`PhysicalBone3D <class_PhysicalBone3D>`. Mỗi node đại diện cho một xương riêng lẻ trong ragdoll.

Mở bản demo platformer trong Godot, sau đó mở scene ``player/player.tscn``. Chọn node ``Skeleton3D``. Một nút skeleton sẽ xuất hiện ở phía trên viewport của trình chỉnh sửa 3D:

.. figure:: img/ragdoll_system_create_physical_skeleton.webp
   :align: center
   :alt: Tạo skeleton vật lý trong trình chỉnh sửa

   Tạo skeleton vật lý trong trình chỉnh sửa

Nhấp vào đó và chọn tùy chọn :menu:`Create Physical Skeleton`. Godot sẽ tạo các node PhysicalBone3D và các hình dạng va chạm cho từng xương trong skeleton, cùng các khớp pin để kết nối chúng với nhau:

.. figure:: img/ragdoll_system_skeleton_scene_tree.webp
   :align: center
   :alt: Cây scene của scene người chơi sau khi tạo skeleton vật lý

   Cây scene của scene người chơi sau khi tạo skeleton vật lý

Một số xương được tạo không cần thiết, chẳng hạn như xương ``MASTER`` trong scene này. Chúng ta sẽ dọn dẹp skeleton bằng cách xóa chúng.

Dọn dẹp và tối ưu skeleton
~~~~~~~~~~~~~~~~~~~~~~~~~~

Mỗi PhysicalBone3D mà engine cần mô phỏng đều gây ra chi phí hiệu năng. Bạn nên xóa mọi xương quá nhỏ để tạo ra khác biệt trong mô phỏng, cũng như tất cả các xương tiện ích.

Ví dụ, nếu xét một nhân vật hình người, bạn không cần có xương vật lý cho từng ngón tay. Thay vào đó, bạn có thể dùng một xương duy nhất cho toàn bộ bàn tay, hoặc một xương cho lòng bàn tay, một xương cho ngón cái và một xương cuối cho bốn ngón còn lại.

Xóa các node PhysicalBone3D này: ``MASTER``, ``waist``, ``neck``, ``headtracker``. Điều này giúp chúng ta có một skeleton được tối ưu và dễ điều khiển ragdoll hơn.

Điều chỉnh các khớp và ràng buộc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau khi điều chỉnh các hình dạng va chạm, ragdoll của bạn gần như đã sẵn sàng. Bây giờ, bạn cần điều chỉnh các khớp pin để có mô phỏng tốt hơn. Theo mặc định, các node PhysicalBone3D được gán một khớp pin không có ràng buộc. Để thay đổi khớp pin, hãy chọn một node PhysicalBone3D và thay đổi loại ràng buộc trong phần :menu:`Joint` của inspector. Tại đó, bạn có thể thay đổi hướng và giới hạn của ràng buộc.

Các khớp cũng có gizmo hiển thị trong trình chỉnh sửa 3D, vì vậy bạn có thể thấy các ràng buộc của chúng hoạt động.

.. figure:: img/ragdoll_system_adjust_joints_inspector.webp
   :align: center
   :alt: Điều chỉnh các khớp trong inspector sau khi chọn một node PhysicalBone3D

   Điều chỉnh các khớp trong inspector sau khi chọn một node PhysicalBone3D

.. tip::

    Để có góc nhìn tốt hơn khi chỉnh sửa các khớp và hình dạng va chạm, bạn có thể làm như sau:

    - Ẩn các node PhysicalBone3D mà bạn hiện không làm việc, để có thể tập trung vào những node đang điều chỉnh.
    - Ẩn MeshInstance3D của nhân vật bằng cách nhấp vào biểu tượng con mắt bên cạnh nó trong dock cây scene.
    - Ẩn các gizmo Skeleton3D để những hình tam giác màu cam đại diện cho skeleton không làm rối viewport, đồng thời vẫn giữ phần còn lại hiển thị. Để làm vậy, hãy nhấp vào :menu:`View > Gizmos > Skeleton3D` ở phía trên viewport của trình chỉnh sửa 3D cho đến khi biểu tượng con mắt hiển thị trạng thái đóng.
    - Tắt môi trường xem trước bằng cách nhấp vào biểu tượng quả địa cầu ở phía trên viewport của trình chỉnh sửa 3D.
    - Đặt thiết lập project **Default Clear Color** thành màu đen hoàn toàn trong Project Settings. Thiết lập này chỉ có hiệu lực khi môi trường xem trước bị tắt.
    - Thay đổi chế độ vẽ gỡ lỗi bằng nút :menu:`Perspective` ở góc trên bên trái của viewport trình chỉnh sửa 3D. Các tùy chọn :menu:`Display Wireframe` và :menu:`Display Overdraw` đặc biệt hữu ích khi điều chỉnh hình dạng va chạm, vì chúng cho phép bạn nhìn xuyên qua mesh gốc.
    - Sử dụng camera trực giao bằng cách nhấp vào các nút :button:`X`/:button:`Y`/:button:`Z` ở góc trên bên phải của viewport trình chỉnh sửa 3D.

Dưới đây là danh sách các khớp hiện có:

- **None:** Không áp dụng bất kỳ ràng buộc nào.
- **ConeJoint:** Khớp cầu. Hữu ích cho vai, hông và cổ.
- **HingeJoint:** Cung cấp ràng buộc góc; hãy hình dung nó giống như bản lề cửa. Hữu ích cho khuỷu tay và đầu gối.
- **PinJoint:** Giữ hai vật thể được kết nối *(default)*. Điều này khiến các xương bị "nhũn xuống", vì vậy bạn nên sử dụng các loại khớp khác cho hầu hết nhân vật.
- **SliderJoint:** Trượt một xương dọc theo xương khác trên một trục cụ thể.
- **6DOFJoint:** Khớp mạnh mẽ nhất, cung cấp cả ràng buộc tuyến tính và góc, nhưng cũng là loại phức tạp nhất để cấu hình.

Nếu không chắc chắn, hãy bắt đầu với HingeJoint và ConeJoint, vì chúng đáp ứng hầu hết các trường hợp sử dụng:

- Đối với HingeJoint, hãy đảm bảo bật **Angular Limit** trong
  phần :menu:`Joint Constraints` của inspector. Sau khi bật, bạn có thể thấy góc mà nó bị giới hạn trong viewport. Bạn có thể xoay PhysicalBone3D để thay đổi trục mà khớp bị giới hạn, sau đó điều chỉnh các góc.
- Đối với ConeJoint, thông thường tốt nhất là giới hạn **Swing Span** trong khoảng từ 20 đến 90 độ, và **Twist Span** trong khoảng từ 20 đến 45 độ.

Điều chỉnh các hình dạng va chạm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nhiệm vụ tiếp theo là điều chỉnh hình dạng va chạm và kích thước của các xương vật lý để khớp với phần cơ thể mà mỗi xương cần mô phỏng.

Bạn nên điều chỉnh các hình dạng va chạm *sau khi* điều chỉnh các khớp và ràng buộc, vì việc xoay một khớp cũng sẽ xoay hình dạng va chạm. Để tránh phải điều chỉnh các hình dạng va chạm hai lần, tốt hơn hết là điều chỉnh các khớp trước.

Lưu ý rằng một node PhysicalBone3D có thể có nhiều hình dạng va chạm làm node con. Điều này hữu ích để biểu diễn các hình dạng đặc biệt phức tạp của các chi vốn cứng.

.. tip::

    Để tạm dừng phát animation trong khi điều chỉnh ragdoll, hãy chọn node ``AnimationTree`` và tắt thuộc tính **Active** trong Inspector. Hãy nhớ bật lại thuộc tính này khi hoàn tất, vì nó điều khiển việc phát animation trong khi chơi.

.. figure:: img/ragdoll_system_adjust_collision_shapes.webp
   :align: center
   :alt: Điều chỉnh các hình dạng va chạm trong trình chỉnh sửa 3D

   Điều chỉnh các hình dạng va chạm trong trình chỉnh sửa 3D

Đây là kết quả cuối cùng:

.. figure:: img/ragdoll_system_result.webp
   :align: center
   :alt: Kết quả sau khi điều chỉnh các khớp và hình dạng va chạm (mesh của người chơi được ẩn để dễ quan sát)

   Kết quả sau khi điều chỉnh các khớp và hình dạng va chạm (mesh của người chơi được ẩn để dễ quan sát)

Mô phỏng ragdoll
----------------

Ragdoll hiện đã sẵn sàng để sử dụng. Để bắt đầu mô phỏng và phát animation ragdoll, bạn cần gọi
phương thức :ref:`PhysicalBoneSimulator3D.physical_bones_start_simulation() <class_PhysicalBoneSimulator3D_method_physical_bones_start_simulation>`. Gắn một script vào node :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>`, là node cha của tất cả các node PhysicalBone3D trong scene của chúng ta, sau đó gọi phương thức này trong phương thức ``_ready`` của script:

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
phương thức :ref:`PhysicalBoneSimulator3D.physical_bones_stop_simulation() <class_PhysicalBoneSimulator3D_method_physical_bones_stop_simulation>`.

.. video:: video/ragdoll_system_full_simulation.webm
    :alt: Full simulation of ragdoll system, with the player falling to the ground
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

Bạn cũng có thể giới hạn mô phỏng chỉ cho một vài xương. Điều này hữu ích để tạo các hiệu ứng như chi ragdoll hoặc các phần gắn thêm có thể tương tác với thế giới. Để thực hiện, hãy truyền tên xương (*không phải* tên node PhysicalBone3D) làm tham số. Để xem tên xương, hãy xem thuộc tính **Bone Name** trong inspector sau khi chọn một node PhysicalBone3D.

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

Lưu ý rằng tên xương không tồn tại sẽ không in ra bất kỳ lỗi hoặc cảnh báo nào. Nếu không có gì xảy ra khi bắt đầu mô phỏng (hoặc nếu toàn bộ cơ thể bị ragdoll thay vì chỉ các xương cụ thể), hãy kiểm tra lại danh sách các xương đã cung cấp.

Sau đây là một ví dụ về mô phỏng ragdoll từng phần:

.. video:: video/ragdoll_system_partial_simulation.webm
    :alt: Partial simulation of ragdoll system, with arms flailing while the player is walking
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tip::

    Để điều khiển mức độ ảnh hưởng của mô phỏng ragdoll từng phần lên animation tổng thể, bạn có thể điều chỉnh thuộc tính **Influence** trong
    node :ref:`PhysicalBoneSimulator3D <class_PhysicalBoneSimulator3D>`, là node cha của tất cả các node PhysicalBone3D. Theo mặc định, thuộc tính này được đặt thành ``1.0``, nghĩa là mô phỏng ragdoll sẽ hoàn toàn ghi đè phần animation còn lại.

Lớp và mặt nạ va chạm
~~~~~~~~~~~~~~~~~~~~~

Hãy đảm bảo thiết lập đúng các lớp và mặt nạ va chạm để capsule của CharacterBody3D không cản trở mô phỏng vật lý. Đồng thời, hãy nhớ điều chỉnh lớp và mặt nạ va chạm trong scene coin để người chơi vẫn có thể nhặt coin:

.. figure:: img/ragdoll_system_collision_layers_masks.webp
   :align: center
   :alt: Các lớp và mặt nạ phải được điều chỉnh thành những giá trị này trong inspector cho từng node

   Các lớp và mặt nạ phải được điều chỉnh thành những giá trị này trong inspector cho từng node

Bạn có thể tìm thấy GridMap trong bản demo platformer 3D tại ``stage/grid_map.scn``. Node Area3D của coin (nơi cần điều chỉnh các lớp và mặt nạ) có thể được tìm thấy tại ``coin/coin.tscn``.

.. tip::

    Để nhanh chóng chọn tất cả các node PhysicalBone3D, hãy nhập ``t:PhysicalBone3D`` vào thanh tìm kiếm ở đầu dock cây scene. Thao tác này sẽ lọc cây scene để chỉ hiển thị các node PhysicalBone3D, cho phép bạn chọn tất cả cùng lúc bằng :kbd:`Shift + Left mouse button` trên mục đầu tiên và mục cuối cùng.

Nếu không thực hiện việc này, va chạm sẽ hoạt động không chính xác vì người chơi sẽ va chạm với ragdoll của chính mình (đang không hoạt động). Điều này có thể khiến người chơi nảy loạn xạ hoặc bị mắc kẹt.

Giống như RigidBody3D, PhysicalBone3D hỗ trợ các ngoại lệ va chạm thông qua code bằng các phương thức :ref:`physical_bones_add_collision_exception() <class_PhysicalBoneSimulator3D_method_physical_bones_add_collision_exception>` và :ref:`physical_bones_remove_collision_exception() <class_PhysicalBoneSimulator3D_method_physical_bones_remove_collision_exception>`. Bạn có thể dùng cách này để ngăn va chạm với một đối tượng cụ thể mà không cần dựa vào các lớp và mặt nạ.

.. seealso::

    Để biết thêm thông tin, hãy xem :ref:`doc_physics_introduction_collision_layers_and_masks`.

.. _`GitHub`: https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer
.. _`Asset Library`: https://godotengine.org/asset-library/asset/2748
.. _`Ragdoll Physics demo`: https://github.com/godotengine/godot-demo-projects/tree/master/3d/ragdoll_physics
