.. _doc_soft_body:

Sử dụng SoftBody3D
==================

Soft body (hay *động lực học soft body*) mô phỏng chuyển động, sự thay đổi hình dạng và các thuộc tính vật lý khác của những vật thể có thể biến dạng. Ví dụ, bạn có thể dùng tính năng này để mô phỏng vải hoặc tạo ra các nhân vật chân thực hơn.

Các cân nhắc về physics engine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hỗ trợ soft body nhìn chung ổn định hơn trong Jolt Physics so với GodotPhysics3D. Bạn có thể chuyển đổi physics engine bằng cách thay đổi **Physics > 3D > Physics Engine** trong Project Settings. Các project được tạo trong Godot 4.6 trở lên mặc định sử dụng Jolt Physics, nhưng các project hiện có sẽ phải được chuyển đổi thủ công.

Ngoài ra, :ref:`physics interpolation <doc_physics_interpolation>` hiện không ảnh hưởng đến soft body. Nếu muốn mô phỏng soft body trông mượt hơn ở framerate cao, bạn sẽ phải tăng thiết lập project **Physics > Common > Physics Ticks per Second**, nhưng điều này sẽ làm giảm hiệu năng.

Thiết lập cơ bản
~~~~~~~~~~~~~~~~

Một node :ref:`SoftBody3D <class_SoftBody3D>` được dùng cho mô phỏng soft body. Không giống các node physics body khác như :ref:`RigidBody3D <class_RigidBody3D>` hoặc :ref:`StaticBody3D <class_StaticBody3D>`, nó **không** có
:ref:`CollisionShape3D <class_CollisionShape3D>` hoặc node con :ref:`MeshInstance3D <class_MeshInstance3D>`. Thay vào đó, collision shape được suy ra từ mesh được gán cho node. Mesh này cũng được dùng trực tiếp để render, nghĩa là bạn không cần tạo node con nào để có một thiết lập hoạt động và hiển thị được.

Chúng ta sẽ tạo một khối lập phương nảy để minh họa cách thiết lập soft body.

Tạo một scene mới với node Node3D làm node gốc. Sau đó, tạo một node SoftBody3D. Thêm một BoxMesh vào thuộc tính **Mesh** của node trong inspector và tăng subdivision của mesh để mô phỏng.

Mức subdivision quyết định độ chính xác của biến dạng; giá trị cao hơn cho phép tạo ra các biến dạng nhỏ hơn và chi tiết hơn, nhưng phải đánh đổi bằng hiệu năng. Trong ví dụ này, chúng ta sẽ đặt giá trị là 3 trên mỗi trục:

.. figure:: img/soft_body_box_mesh.webp
   :align: center
   :alt: Điều chỉnh các thuộc tính BoxMesh trong inspector

   Điều chỉnh các thuộc tính BoxMesh trong inspector

Bây giờ, hãy đặt các tham số để đạt được loại soft body bạn mong muốn. Hãy cố gắng giữ **Simulation Precision** trên 5; nếu không, soft body có thể bị sụp đổ.

.. figure:: img/soft_body_inspector.webp
   :align: center
   :alt: Điều chỉnh các thuộc tính mô phỏng SoftBody3D trong inspector

   Điều chỉnh các thuộc tính mô phỏng SoftBody3D trong inspector

.. note::

    Hãy cẩn thận khi điều chỉnh một số tham số, vì một số giá trị có thể dẫn đến kết quả bất thường. Ví dụ, nếu hình dạng không hoàn toàn khép kín và bạn đặt pressure lớn hơn ``0.0``, soft body sẽ bay quanh như một túi nhựa dưới gió mạnh.

Chạy scene để xem mô phỏng. Dưới đây là ví dụ về kết quả mong đợi:

.. video:: video/soft_body_box_simulation.webm
    :alt: Soft body box simulation example
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tip::

    Để cải thiện kết quả mô phỏng, hãy tăng **Simulation Precision**. Điều này có thể cải thiện đáng kể, nhưng phải đánh đổi bằng hiệu năng.

    Ngoài ra, bạn có thể tăng thiết lập project **Physics > Common > Physics Ticks per Second**, thiết lập này cũng sẽ ảnh hưởng đến chất lượng mô phỏng soft body.

Mô phỏng áo choàng
~~~~~~~~~~~~~~~~~~

Hãy tạo một chiếc áo choàng trong bản demo Platformer 3D.

.. note::

    Bạn có thể tải bản demo Platformer 3D từ `GitHub <https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer>`_ hoặc `Asset Library <https://godotengine.org/asset-library/asset/2748>`_.

Mở scene ``player/player.tscn``, thêm một node ``SoftBody3D`` bên dưới node gốc, sau đó gán một resource PlaneMesh cho node này trong thuộc tính **Mesh**.

Mở các thuộc tính của PlaneMesh và đặt kích thước là ``(0.5, 1.0)``, sau đó đặt **Subdivide Width** và **Subdivide Depth** thành ``5``. Điều chỉnh vị trí và rotation của node SoftBody3D để mặt phẳng nằm gần lưng nhân vật. Kết quả sẽ tương tự như sau:

.. figure:: img/soft_body_cloak_subdivide.webp
   :align: center
   :alt: Chia nhỏ PlaneMesh và đặt nó lên lưng nhân vật

   Chia nhỏ PlaneMesh và đặt nó lên lưng nhân vật

.. tip::

    Subdivision tạo ra một mesh có nhiều tessellation hơn để mô phỏng tốt hơn. Tuy nhiên, mức subdivision cao hơn sẽ ảnh hưởng đến hiệu năng. Hãy tìm sự cân bằng giữa hiệu năng và chất lượng. Điều này phụ thuộc vào số lượng mô phỏng soft body mà bạn dự kiến sẽ hoạt động cùng lúc, cũng như khoảng cách giữa camera và soft body.

Thêm một node :ref:`BoneAttachment3D <class_BoneAttachment3D>` bên dưới node skeleton và chọn bone Neck để gắn áo choàng vào skeleton của nhân vật.

.. note::

    Node BoneAttachment3D được dùng để gắn các object vào một bone của armature. Object được gắn sẽ đi theo chuyển động của bone. Ví dụ, vũ khí mà nhân vật cầm có thể được gắn theo cách này.

    Hiện tại, **không** di chuyển node SoftBody3D vào bên dưới node BoneAttachment3D. Thay vào đó, chúng ta sẽ cấu hình *các điểm được ghim* để chúng đi theo node BoneAttachment3D.

.. figure:: img/soft_body_cloak_bone_attach.webp
   :align: center
   :alt: Cấu hình node BoneAttachment3D trong inspector

   Cấu hình node BoneAttachment3D trong inspector

Để tạo các điểm được ghim, hãy chọn các đỉnh phía trên trong node SoftBody3D. Một điểm được ghim sẽ hiển thị màu xanh lam trong viewport của trình chỉnh sửa 3D:

.. figure:: img/soft_body_cloak_pinned.webp
   :align: center
   :alt: Ghim các điểm của SoftBody3D trong inspector

   Ghim các điểm của SoftBody3D trong inspector

Các joint được ghim có thể được tìm thấy trong phần **Attachments** của SoftBody3D, nằm bên dưới phần **Collision**, phần này phải được mở rộng trước. Chọn node BoneAttachment3D làm **Spatial Attachment Path** cho từng joint được ghim. Các joint được ghim giờ đã được gắn vào cổ.

.. tip::

    Để gán các thuộc tính nhanh hơn, bạn có thể kéo và thả node BoneAttachment3D từ scene tree dock vào trường thuộc tính **Spatial Attachment Path**.

Lưu ý rằng bạn có thể phải bỏ chọn rồi chọn lại node SoftBody3D để phần **Attachments** xuất hiện.

.. figure:: img/soft_body_cloak_pinned_attach.webp
   :align: center
   :alt: Cấu hình các điểm được ghim để gắn vào node BoneAttachment3D trong inspector của SoftBody3D

   Cấu hình các điểm được ghim để gắn vào node BoneAttachment3D trong inspector của SoftBody3D

Bước cuối cùng là tránh hiện tượng clipping bằng cách thêm CharacterBody3D ``Player`` (node gốc của scene) vào thuộc tính **Parent Collision Ignore** của SoftBody3D.

.. figure:: img/soft_body_cloak_ignore.webp
   :align: center
   :alt: Thiết lập ngoại lệ collision trong inspector của SoftBody3D

   Thiết lập ngoại lệ collision trong inspector của SoftBody3D

Chạy scene và áo choàng sẽ được mô phỏng chính xác.

.. figure:: img/soft_body_cloak_finish.webp
   :align: center
   :alt: Kết quả cuối cùng khi chạy scene chính của project

   Kết quả cuối cùng khi chạy scene chính của dự án

Phần này trình bày các thiết lập cơ bản của mô phỏng soft body. Hãy thử nghiệm với các tham số để đạt được hiệu ứng mong muốn khi tạo game.

.. note::

    Áo choàng sẽ không xuất hiện khi được nhìn từ một số góc nhất định do cơ chế loại bỏ mặt sau (backface culling). Để khắc phục, bạn có thể vô hiệu hóa cơ chế loại bỏ mặt sau bằng cách gán một StandardMaterial3D mới, sau đó đặt chế độ cull thành **Disabled**. Thao tác này sẽ khiến material hiển thị cả hai mặt của mặt phẳng.

Sử dụng mesh đã import
~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn **Save to File** trong hộp thoại Advanced Import Settings cho phép bạn lưu một mesh vào tệp tài nguyên độc lập, sau đó có thể gắn tệp này vào các node SoftBody3D.

Bạn cũng có thể muốn tắt việc tạo LOD hoặc thay đổi các tùy chọn tạo LOD khi import một mesh để sử dụng với SoftBody3D. Các thiết lập import mặc định sẽ tạo ra một LOD hợp nhất những mặt liền kề gần như phẳng so với nhau, ngay cả khi khoảng cách render rất gần. Điều này hoạt động tốt với các mesh tĩnh, nhưng thường không phù hợp khi sử dụng với SoftBody3D nếu bạn muốn các mặt này có thể uốn cong và di chuyển tương đối với nhau, thay vì được render dưới dạng một mặt phẳng duy nhất.

Xem :ref:`doc_importing_3d_scenes_import_configuration` và :ref:`doc_mesh_lod` để biết thêm chi tiết.

.. _`GitHub`: https://github.com/godotengine/godot-demo-projects/tree/master/3d/platformer
.. _`the Asset Library`: https://godotengine.org/asset-library/asset/2748
