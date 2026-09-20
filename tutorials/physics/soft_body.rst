.. _doc_soft_body:

Sử dụng SoftBody3D
==================

Các vật thể mềm (hay *động lực học vật thể mềm*) mô phỏng chuyển động, sự thay đổi hình dạng và các thuộc tính vật lý khác của những vật thể có thể biến dạng. Ví dụ, tính năng này có thể được dùng để mô phỏng vải hoặc tạo ra các nhân vật chân thực hơn.

Các lưu ý về physics engine
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc hỗ trợ vật thể mềm nhìn chung ổn định hơn trong Jolt Physics so với GodotPhysics3D. Bạn có thể chuyển đổi physics engine bằng cách thay đổi **Physics > 3D > Physics Engine** trong Project Settings. Các project được tạo trong Godot 4.6 trở lên sẽ sử dụng Jolt Physics theo mặc định, nhưng với các project hiện có, bạn sẽ phải chuyển đổi thủ công.

Ngoài ra, :ref:`physics interpolation <doc_physics_interpolation>` hiện không ảnh hưởng đến các vật thể mềm. Nếu muốn mô phỏng vật thể mềm trông mượt hơn ở framerate cao hơn, bạn sẽ phải tăng thiết lập project **Physics > Common > Physics Ticks per Second**, việc này sẽ làm giảm hiệu năng.

Thiết lập cơ bản
~~~~~~~~~~~~~~~~

Một node :ref:`SoftBody3D <class_SoftBody3D>` được dùng để mô phỏng vật thể mềm. Không giống các node physics body khác như :ref:`RigidBody3D <class_RigidBody3D>` hoặc :ref:`StaticBody3D <class_StaticBody3D>`, nó **không có một
:ref:`CollisionShape3D <class_CollisionShape3D>` or a :ref:`MeshInstance3D <class_MeshInstance3D>`
node con. Thay vào đó, collision shape được suy ra từ mesh được gán cho node. Mesh này cũng được dùng trực tiếp để rendering, nghĩa là bạn không cần tạo node con nào để có một thiết lập hoạt động và hiển thị được.

Chúng ta sẽ tạo một khối lập phương nảy để minh họa cách thiết lập vật thể mềm.

Tạo một scene mới với node Node3D làm node gốc. Sau đó, tạo một node SoftBody3D. Thêm một BoxMesh vào thuộc tính **Mesh** của node trong inspector và tăng subdivision của mesh để mô phỏng.

Mức subdivision quyết định độ chính xác của biến dạng, trong đó các giá trị cao hơn cho phép tạo ra những biến dạng nhỏ hơn và chi tiết hơn, nhưng phải đánh đổi bằng hiệu năng. Trong ví dụ này, chúng ta sẽ đặt giá trị là 3 trên mỗi trục:

.. figure:: img/soft_body_box_mesh.webp
   :align: center
   :alt: Adjusting BoxMesh properties in the inspector

   Adjusting BoxMesh properties in the inspector

Bây giờ, hãy thiết lập các tham số để đạt được loại vật thể mềm mà bạn mong muốn. Hãy cố gắng giữ **Simulation Precision** trên 5; nếu không, vật thể mềm có thể bị sụp đổ.

.. figure:: img/soft_body_inspector.webp
   :align: center
   :alt: Adjusting SoftBody3D simulation properties in the inspector

   Adjusting SoftBody3D simulation properties in the inspector

.. note::

    Hãy cẩn thận khi xử lý một số tham số, vì một số giá trị có thể dẫn đến kết quả bất thường. Ví dụ, nếu hình dạng không hoàn toàn khép kín và bạn đặt pressure lớn hơn ``0.0``, vật thể mềm sẽ bay vòng quanh như một chiếc túi nhựa trong gió mạnh.

Chạy scene để xem mô phỏng. Đây là ví dụ về kết quả mà bạn sẽ thấy:

.. video:: video/soft_body_box_simulation.webm
    :alt: Soft body box simulation example
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tip::

    Để cải thiện kết quả mô phỏng, hãy tăng **Simulation Precision**. Điều này có thể cải thiện đáng kể, nhưng phải đánh đổi bằng hiệu năng.

    Ngoài ra, bạn có thể tăng thiết lập project **Physics > Common > Physics Ticks per Second**, thiết lập này cũng sẽ ảnh hưởng đến chất lượng mô phỏng vật thể mềm.

Mô phỏng áo choàng
~~~~~~~~~~~~~~~~~~

Hãy tạo một chiếc áo choàng trong demo Platformer 3D.

.. note::

    Bạn có thể tải demo Platformer 3D từ `GitHub <https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer>`_ hoặc `the Asset Library <https://godotengine.org/asset-library/asset/2748>`_.

Mở scene ``player/player.tscn``, thêm một node ``SoftBody3D`` bên dưới node gốc, sau đó gán một resource PlaneMesh cho node đó trong thuộc tính **Mesh**.

Mở các thuộc tính của PlaneMesh và đặt kích thước là ``(0.5, 1.0)``, sau đó đặt **Subdivide Width** và **Subdivide Depth** thành ``5``. Điều chỉnh vị trí và rotation của node SoftBody3D để mặt phẳng nằm gần lưng của nhân vật. Kết quả sẽ tương tự như sau:

.. figure:: img/soft_body_cloak_subdivide.webp
   :align: center
   :alt: Subdividing the PlaneMesh and placing it on the character's back

   Subdividing the PlaneMesh and placing it on the character's back

.. tip::

    Subdivision tạo ra một mesh được tessellate nhiều hơn để mô phỏng tốt hơn. Tuy nhiên, mức subdivision cao hơn sẽ ảnh hưởng đến hiệu năng. Hãy cố gắng tìm sự cân bằng giữa hiệu năng và chất lượng. Điều này phụ thuộc vào số lượng mô phỏng vật thể mềm mà bạn dự kiến sẽ hoạt động tại một thời điểm, cũng như khoảng cách giữa camera và vật thể mềm.

Thêm một node :ref:`BoneAttachment3D <class_BoneAttachment3D>` bên dưới node skeleton và chọn bone Neck để gắn áo choàng vào skeleton của nhân vật.

.. note::

    Node BoneAttachment3D được dùng để gắn các object vào một bone của armature. Object được gắn sẽ đi theo chuyển động của bone. Ví dụ, vũ khí mà nhân vật cầm có thể được gắn theo cách này.

    Hiện tại, **không** di chuyển node SoftBody3D vào bên dưới node BoneAttachment3D. Thay vào đó, chúng ta sẽ cấu hình các *pinned points* của nó để đi theo node BoneAttachment3D.

.. figure:: img/soft_body_cloak_bone_attach.webp
   :align: center
   :alt: Configuring the BoneAttachment3D node in the inspector

   Configuring the BoneAttachment3D node in the inspector

Để tạo pinned points, hãy chọn các vertex phía trên trong node SoftBody3D. Một pinned point sẽ có màu xanh dương trong viewport của trình chỉnh sửa 3D:

.. figure:: img/soft_body_cloak_pinned.webp
   :align: center
   :alt: Pinning the SoftBody3D's points in the inspector

   Pinning the SoftBody3D's points in the inspector

Bạn có thể tìm thấy các pinned joint trong phần **Attachments** của SoftBody3D, nằm bên dưới phần **Collision**, phần này trước tiên phải được mở rộng. Chọn node BoneAttachment3D làm **Spatial Attachment Path** cho từng pinned joint. Các pinned joint hiện đã được gắn vào cổ.

.. tip::

    Để gán các thuộc tính nhanh hơn, bạn có thể kéo-thả node BoneAttachment3D từ scene tree dock vào trường thuộc tính **Spatial Attachment Path**.

Lưu ý rằng bạn có thể phải bỏ chọn rồi chọn lại node SoftBody3D để phần **Attachments** xuất hiện.

.. figure:: img/soft_body_cloak_pinned_attach.webp
   :align: center
   :alt: Configuring pinned points to be attached to the BoneAttachment3D node in the SoftBody3D inspector

   Configuring pinned points to be attached to the BoneAttachment3D node in the SoftBody3D inspector

Bước cuối cùng là tránh clipping bằng cách thêm CharacterBody3D ``Player`` (node gốc của scene) vào thuộc tính **Parent Collision Ignore** của SoftBody3D.

.. figure:: img/soft_body_cloak_ignore.webp
   :align: center
   :alt: Setting up the collision exception in the SoftBody3D inspector

   Setting up the collision exception in the SoftBody3D inspector

Chạy scene và áo choàng sẽ được mô phỏng chính xác.

.. figure:: img/soft_body_cloak_finish.webp
   :align: center
   :alt: Final result when running the project's main scene

   Final result when running the project's main scene

Đây là các thiết lập cơ bản của mô phỏng vật thể mềm. Hãy thử nghiệm với các tham số để đạt được hiệu ứng mà bạn mong muốn khi tạo game.

.. note::

    Áo choàng sẽ không xuất hiện khi nhìn từ một số góc nhất định do backface culling. Để khắc phục, bạn có thể tắt backface culling bằng cách gán một StandardMaterial3D mới, sau đó đặt chế độ cull thành **Disabled**. Điều này sẽ khiến material rendering cả hai mặt của mặt phẳng.

Sử dụng mesh đã import
~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn **Save to File** trong hộp thoại Advanced Import Settings cho phép bạn lưu mesh vào một resource file độc lập, sau đó có thể gắn resource này vào các node SoftBody3D.

Bạn cũng có thể muốn tắt tính năng tạo LOD hoặc thay đổi các tùy chọn tạo LOD khi import mesh để sử dụng với SoftBody3D. Các thiết lập import mặc định sẽ tạo ra một LOD gộp các mặt liền kề gần như phẳng so với nhau, ngay cả ở khoảng cách rendering rất gần. Cách này hoạt động tốt với các mesh tĩnh, nhưng thường không phù hợp khi sử dụng với SoftBody3D nếu bạn muốn các mặt này có thể uốn cong và chuyển động tương đối với nhau, thay vì được rendering như một mặt phẳng duy nhất.

Xem :ref:`doc_importing_3d_scenes_import_configuration` và :ref:`doc_mesh_lod` để biết thêm chi tiết.
