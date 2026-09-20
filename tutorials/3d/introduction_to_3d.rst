.. _doc_introduction_to_3d:

Giới thiệu về 3D
================

Việc tạo một game 3D có thể khá khó khăn. Tọa độ Z bổ sung khiến nhiều kỹ thuật thông thường từng giúp việc tạo game 2D trở nên đơn giản không còn hoạt động. Để hỗ trợ quá trình chuyển đổi này, cần lưu ý rằng Godot sử dụng các API tương tự nhau cho 2D và 3D. Hầu hết các node đều giống nhau và hiện diện trong cả phiên bản 2D lẫn 3D. Trên thực tế, bạn nên xem qua tutorial về platformer 3D hoặc các tutorial về nhân vật kinematic 3D, vì chúng gần như giống hệt các phiên bản tương ứng trong 2D.

.. figure:: img/godot-tps-demo.webp
   :align: center
   :alt: An example 3D game demo created using Godot

   Godot Third Person Shooter (TPS) Demo, available on the
   `Github repository <https://github.com/godotengine/tps-demo>`__ hoặc
   :ref:`Asset Library <doc_project_manager_downloading_demos>`.

Trong 3D, toán học phức tạp hơn một chút so với 2D. Để tìm hiểu phần toán học liên quan dành cho các nhà phát triển game, không phải các nhà toán học hay kỹ sư, hãy xem :ref:`doc_vector_math` và :ref:`doc_using_transforms`.

Không gian làm việc 3D
----------------------

Việc chỉnh sửa các scene 3D được thực hiện trong không gian làm việc 3D. Bạn có thể chọn không gian làm việc này theo cách thủ công, nhưng nó sẽ được tự động chọn khi một node Node3D được chọn.

.. image:: img/tuto_3d3.webp

Tương tự như 2D, các tab bên dưới bộ chọn không gian làm việc được dùng để chuyển đổi giữa các scene hiện đang mở hoặc tạo scene mới bằng nút dấu cộng (+). Các dock bên trái và bên phải hẳn sẽ quen thuộc nếu bạn đã xem :ref:`editor introduction <doc_editor_introduction>`.

Bên dưới bộ chọn scene là thanh công cụ chính, và bên dưới thanh công cụ chính là viewport 3D.

Thanh công cụ chính
~~~~~~~~~~~~~~~~~~~

Một số nút trong thanh công cụ chính giống với các nút trong không gian làm việc 2D. Khi di con trỏ chuột lên một nút trong một giây, một phần giải thích ngắn sẽ xuất hiện cùng với phím tắt. Một số nút có thể có thêm chức năng nếu nhấn thêm một phím khác. Dưới đây là phần tóm tắt chức năng chính của từng nút cùng phím tắt mặc định, theo thứ tự từ trái sang phải:

.. image:: img/3d_toolbar.webp

- **Transform Mode** (:kbd:`Q`): Bật chế độ kết hợp di chuyển + xoay cho các node được chọn. - **Move Mode** (:kbd:`W`): Bật chế độ di chuyển (hoặc tịnh tiến) cho các node được chọn. Xem :ref:`doc_introduction_to_3d_space_and_manipulation` để biết thêm chi tiết. - **Rotate Mode** (:kbd:`E`): Bật chế độ xoay cho các node được chọn. Xem
  :ref:`doc_introduction_to_3d_space_and_manipulation` for more details.
- **Scale Mode** (:kbd:`R`): Bật tính năng scale và hiển thị các gizmo scale trên các trục khác nhau cho các node được chọn. Xem :ref:`doc_introduction_to_3d_space_and_manipulation` để biết thêm chi tiết. - **Select Mode** (:kbd:`V`): Cho phép chọn các node trong viewport. Nhấp chuột trái vào một node để chọn node đó. Nhấp chuột trái và kéo một hình chữ nhật sẽ chọn tất cả các node nằm trong ranh giới của hình chữ nhật sau khi thả chuột. Giữ :kbd:`Shift` trong khi chọn để thêm các node vào vùng chọn. Nhấp vào một node đã chọn trong khi giữ :kbd:`Shift` sẽ bỏ chọn node đó. Trong chế độ này, bạn có thể sử dụng các gizmo để di chuyển hoặc xoay. - **Show the list of selectable nodes at the clicked position**: Như mô tả cho thấy, tùy chọn này cung cấp danh sách các node có thể chọn tại vị trí được nhấp dưới dạng context menu, nếu có nhiều hơn một node trong khu vực được nhấp. - **Lock** (:kbd:`Ctrl + L`) các node được chọn, ngăn việc chọn và di chuyển chúng trong viewport. Nhấp lại vào nút (hoặc sử dụng :kbd:`Ctrl + Shift + L`) để mở khóa các node được chọn. Các node bị khóa chỉ có thể được chọn trong scene tree. Bạn có thể dễ dàng nhận biết chúng nhờ biểu tượng ổ khóa bên cạnh tên node trong scene tree. Nhấp vào biểu tượng ổ khóa này cũng sẽ mở khóa các node. - **Group selected nodes** (:kbd:`Ctrl + G`). Cho phép chọn node gốc nếu bất kỳ node con nào đang được chọn. Sử dụng :kbd:`Ctrl + G` để bỏ nhóm chúng. Ngoài ra, nhấp vào nút bỏ nhóm trong scene tree cũng thực hiện thao tác tương tự. - **Ruler Mode** (:kbd:`M`): Khi được bật, bạn có thể nhấp và kéo để đo khoảng cách trong scene theo mét. - **Use Local Space** (:kbd:`T`): Khi được bật, các gizmo của một node được vẽ theo góc xoay hiện tại của node thay vì :ref:`global viewport axes <doc_introduction_to_3d_coordinate_system>`. - **Use Snap** (:kbd:`Y`): Khi được bật, thao tác di chuyển và xoay sẽ snap theo grid. Bạn cũng có thể tạm thời bật snap bằng :kbd:`Ctrl` trong khi thực hiện thao tác. Các thiết lập để thay đổi tùy chọn snap được giải thích bên dưới. - **Use Trackball** (:kbd:`U`): Khi được bật, kéo phần trung tâm của một node (được biểu thị bằng một vùng sáng dạng đĩa tia tinh tế) sẽ xoay node giống như một trackball vật lý. - **Preserve Children Transform** (:kbd:`P`): Khi được bật, việc biến đổi một node sẽ giữ nguyên transform toàn cục của các node con. - **Toggle preview sunlight**: Nếu scene không có DirectionalLight3D, có thể sử dụng bản xem trước ánh sáng mặt trời làm nguồn sáng. Xem
  :ref:`doc_introduction_to_3d_preview_environment_light` for more details.
- **Toggle preview environment**: Nếu scene không có WorldEnvironment, có thể sử dụng bản xem trước môi trường làm placeholder. Xem
  :ref:`doc_introduction_to_3d_preview_environment_light` for more details.
- **Edit Sun and Environment Settings (three dots)**: Mở menu để cấu hình các thiết lập ánh sáng mặt trời và môi trường xem trước. Xem :ref:`doc_introduction_to_3d_preview_environment_light` để biết thêm chi tiết.

- **Transform menu**: Có ba tùy chọn:

   - *Snap Object to Floor*: Snap một đối tượng vào một mặt sàn cố định. - *Transform Dialog*: Mở hộp thoại để điều chỉnh thủ công các tham số transform (tịnh tiến, xoay, scale và transform). - *Snap Settings*: Cho phép thay đổi các thiết lập snap cho transform, xoay (theo độ) và scale (theo phần trăm).

- **View menu**: Điều khiển các tùy chọn hiển thị và bật thêm các viewport:

.. image:: img/tuto_3d6.webp

Trong menu này, bạn cũng có thể hiển thị/ẩn các grid, mặc định được đặt ở kích thước 1x1 mét, và điểm gốc, nơi các đường trục màu xanh dương, xanh lá và đỏ giao nhau. Ngoài ra, bạn có thể bật/tắt các loại gizmo cụ thể trong menu này.

.. image:: img/tuto_3d6_2.webp

Con mắt mở có nghĩa là gizmo đang hiển thị, con mắt đóng có nghĩa là gizmo bị ẩn. Con mắt hé mở có nghĩa là gizmo cũng hiển thị xuyên qua các bề mặt đục.

Nhấp vào *Settings* trong view menu này sẽ mở một cửa sổ để thay đổi tham số *Vertical Field of View (VFOV)* (theo độ), các giá trị *Z-Near* và *Z-Far*.

Bên cạnh View menu có thể xuất hiện thêm các nút. Trong hình ảnh thanh công cụ ở đầu chương này, nút *Mesh* bổ sung xuất hiện vì một MeshInstance3D đang được chọn. Menu này cung cấp một số thao tác hoặc công cụ nhanh để làm việc với một node hoặc vùng chọn cụ thể.

View menu của viewport
~~~~~~~~~~~~~~~~~~~~~~

Bên dưới công cụ *Select*, trong viewport 3D, nhấp vào dấu ba chấm sẽ mở **View menu** cho viewport. Bạn cũng có thể ẩn tất cả các gizmo đang hiển thị trong view 3D của editor thông qua menu này:

.. image:: img/tuto_3d6_1.webp

Menu này cũng hiển thị loại view hiện tại và cho phép nhanh chóng điều chỉnh góc nhìn của viewport. Ngoài ra, menu cung cấp các tùy chọn để thay đổi diện mạo của các node bên trong viewport.

.. _doc_introduction_to_3d_coordinate_system:

Hệ tọa độ
~~~~~~~~~

Godot sử dụng hệ `metric <https://en.wikipedia.org/wiki/Metric_system>`__ cho mọi thứ trong 3D, trong đó 1 unit tương đương 1 mét. Physics và các lĩnh vực khác được tinh chỉnh theo tỷ lệ này. Vì vậy, cố gắng sử dụng một tỷ lệ khác thường là một ý tưởng tồi (trừ khi bạn biết mình đang làm gì).

Khi làm việc với các asset 3D, tốt nhất luôn làm việc ở đúng tỷ lệ (đặt unit thành metric trong phần mềm tạo mô hình 3D của bạn). Godot cho phép scale sau khi import và mặc dù tính năng này hoạt động trong hầu hết trường hợp, trong một số tình huống hiếm gặp, nó có thể gây ra vấn đề về độ chính xác số dấu phẩy động (và do đó gây ra glitch hoặc artifact) ở các khu vực nhạy cảm như rendering hoặc physics. Hãy đảm bảo các artist của bạn luôn làm việc ở đúng tỷ lệ!

Tọa độ Y được dùng cho hướng "lên". Đối với các trục ngang X/Z, Godot sử dụng hệ tọa độ **thuận tay phải**. Điều này có nghĩa là đối với hầu hết các đối tượng cần căn chỉnh (chẳng hạn như đèn hoặc camera), trục Z được dùng làm hướng "chỉ về phía trước". Quy ước này có nghĩa gần đúng rằng:

-  **X** là hai bên - **Y** là lên/xuống - **Z** là trước/sau

Xem biểu đồ này để so sánh với các phần mềm 3D khác:

.. figure:: img/introduction_to_3d_coordinate_systems.webp
   :align: center
   :alt: 3D coordinate systems comparison chart

   Image by `Freya Holmér <https://twitter.com/FreyaHolmer>`__


.. _doc_introduction_to_3d_space_and_manipulation:

Gizmo không gian và thao tác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc di chuyển, xoay và scale các đối tượng trong view 3D được thực hiện thông qua các gizmo thao tác. Mỗi trục được biểu thị bằng một màu: Đỏ, Xanh lá, Xanh dương lần lượt đại diện cho X, Y, Z. Quy ước này cũng áp dụng cho grid và các gizmo khác (cũng như ngôn ngữ shader, thứ tự các thành phần của Vector3, Color, v.v.).

.. image:: img/tuto_3d5.webp

Một số keybinding hữu ích:

-  Để snap vị trí hoặc góc xoay, nhấn :kbd:`Ctrl` trong khi di chuyển, scale hoặc xoay. - Để căn giữa view theo đối tượng được chọn, nhấn :kbd:`F`.

Trong viewport, bạn có thể nhấp và giữ các mũi tên để di chuyển đối tượng trên một trục. Bạn có thể nhấp và giữ các cung để xoay đối tượng. Để khóa một trục và tự do di chuyển đối tượng trên hai trục còn lại, hãy nhấp, giữ và kéo các hình chữ nhật màu.

Nếu chuyển transform mode từ *Select Mode* sang *Scale Mode*, các mũi tên sẽ được thay thế bằng các hình lập phương, có thể kéo để scale một đối tượng như thể đối tượng đang được di chuyển.

Điều hướng môi trường 3D
~~~~~~~~~~~~~~~~~~~~~~~~

Trong môi trường 3D, việc điều chỉnh góc nhìn hoặc góc mà bạn dùng để xem scene thường rất quan trọng. Trong Godot, bạn có thể điều hướng môi trường 3D trong viewport (hoặc spatial editor) theo nhiều cách.

Các điều khiển điều hướng scene 3D mặc định tương tự như Blender (nhằm tạo ra sự nhất quán nhất định trong free software pipeline), nhưng có các tùy chọn để tùy chỉnh nút chuột và hành vi sao cho tương tự các công cụ khác trong Editor Settings. Để thay đổi các điều khiển thành điều khiển của Maya hoặc Modo, bạn có thể đi đến **Editor Settings > Editors > 3D**. Sau đó, trong mục *Navigation*, tìm kiếm *Navigation Scheme*.

.. image:: img/tuto_3d4.webp

Với các thiết lập mặc định, những phím tắt sau đây điều khiển cách bạn điều hướng trong viewport:

Nhấn nút chuột giữa và kéo chuột cho phép bạn xoay quanh tâm của nội dung trên màn hình.

Bạn cũng có thể nhấp chuột trái và giữ trên manipulator gizmo nằm ở phía trên bên phải của viewport để xoay quanh tâm:

.. image:: img/tuto_3d_gizmo.webp

Nhấp chuột trái vào một trong các vòng tròn màu sẽ đặt view thành orthogonal đã chọn và menu View của viewport sẽ được cập nhật tương ứng.

.. image:: img/tuto_3d_updated_view_menu.webp

Nếu view *Perspective* được bật trên viewport (có thể thấy trong menu View của viewport, không phải menu View trên thanh công cụ chính), giữ nút chuột phải trên viewport hoặc nhấn :kbd:`Shift + F` sẽ chuyển sang chế độ "free-look". Trong chế độ này, bạn có thể di chuyển chuột để quan sát xung quanh, sử dụng :kbd:`W` :kbd:`A`
:kbd:`S` :kbd:`D` keys to fly around the view, :kbd:`E` to go up, and :kbd:`Q` to
đi xuống. Để tắt chế độ này, thả nút chuột phải hoặc nhấn
:kbd:`Shift + F` again.

Trong chế độ free-look, bạn có thể tạm thời tăng tốc độ bay bằng :kbd:`Shift` hoặc giảm tốc độ bằng :kbd:`Alt`. Để thay đổi và giữ nguyên hệ số tốc độ, hãy dùng :kbd:`mouse wheel up` hoặc :kbd:`mouse wheel down` để lần lượt tăng hoặc giảm hệ số này.

Trong chế độ orthogonal, giữ nút chuột phải sẽ thay vào đó pan view. Sử dụng :kbd:`Keypad 5` để chuyển đổi giữa view perspective và orthogonal.

Sử dụng các phím tắt transform kiểu Blender
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.2, bạn có thể bật các phím tắt kiểu Blender để translate, rotate và scale node. Trong Blender, các phím tắt này là:

- :kbd:`G` để translate - :kbd:`R` để rotate - :kbd:`S` để scale

Sau khi nhấn một phím tắt trong khi viewport của trình chỉnh sửa 3D đang được focus, hãy di chuyển chuột hoặc nhập một số để di chuyển các node đã chọn theo khoảng cách được chỉ định trong các đơn vị 3D. Bạn có thể giới hạn chuyển động theo một axis cụ thể bằng cách chỉ định axis dưới dạng một chữ cái, sau đó là khoảng cách (nếu nhập giá trị bằng bàn phím).

Ví dụ, để di chuyển vùng chọn lên trên 2.5 đơn vị, hãy nhập lần lượt chuỗi sau (Y+ là hướng lên trong Godot):

:kbd:`G`-:kbd:`Y`-:kbd:`2`-:kbd:`.`-:kbd:`5`-:kbd:`Enter`

Để sử dụng các phím tắt transform kiểu Blender trong Godot, hãy đi tới tab **Shortcuts** trong Editor Settings, sau đó trong phần Spatial Editor:

- Gán **Begin Translate Transformation** cho :kbd:`G`. - Gán **Begin Rotate Transformation** cho :kbd:`R`. - Gán **Begin Scale Transformation** cho :kbd:`S`. - Cuối cùng, bỏ gán **Scale Mode** để phím tắt của nó không xung đột với **Begin Rotate Transformation**.

Node3D node
-----------

:ref:`Node2D <class_Node2D>` is the base node for 2D.
:ref:`Control <class_Control>` is the base node for everything GUI.
Theo cách hiểu này, 3D engine sử dụng node :ref:`Node3D <class_Node3D>` cho mọi thứ liên quan đến 3D.

.. image:: img/tuto_3d1.webp

Node3D có một local transform, tương đối so với parent node (miễn là parent node cũng thuộc kiểu **or inherits from** Node3D). Transform này có thể được truy cập dưới dạng 3×4
:ref:`Transform3D <class_Transform3D>`, or as 3 :ref:`Vector3 <class_Vector3>`
các member đại diện cho vị trí, phép xoay Euler (các góc X, Y và Z) và scale.

.. image:: img/tuto_3d2.webp

Nội dung 3D
-----------

Không giống 2D, trong đó việc tải nội dung hình ảnh và vẽ khá đơn giản, 3D phức tạp hơn một chút. Nội dung cần được tạo bằng các công cụ 3D chuyên dụng (còn gọi là công cụ Digital Content Creation, hay DCC) và được export sang một exchange file format để import vào Godot. Điều này là cần thiết vì các định dạng 3D không được chuẩn hóa như hình ảnh.

Các model được tạo thủ công (bằng phần mềm modeling 3D)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. FIXME: Cần cập nhật để mô tả đúng workflow Godot 3.x (trước đây tham chiếu đến một importer doc_importing_3d_meshes không tồn tại).

Có thể import các model 3D được tạo bằng công cụ bên ngoài vào Godot. Tùy thuộc vào định dạng, bạn có thể import toàn bộ scene (chính xác như trong phần mềm modeling 3D), bao gồm animation, skeletal rig, blend shape, hoặc dưới dạng các resource đơn giản.

.. seealso:: See :ref:`doc_importing_3d_scenes` for more on importing.

Geometry được tạo
~~~~~~~~~~~~~~~~~

Có thể tạo geometry tùy chỉnh bằng cách sử dụng
:ref:`ArrayMesh <class_ArrayMesh>` resource directly. Simply create your arrays
và sử dụng hàm :ref:`ArrayMesh.add_surface_from_arrays() <class_ArrayMesh_method_add_surface_from_arrays>`. Một helper class cũng có sẵn là :ref:`SurfaceTool <class_SurfaceTool>`, cung cấp API và các helper đơn giản hơn để indexing, tạo normals, tangents, v.v.

Trong mọi trường hợp, phương pháp này nhằm tạo static geometry (các model không được cập nhật thường xuyên), vì việc tạo các vertex array và gửi chúng đến 3D API có chi phí hiệu năng đáng kể.

.. note:: To learn about prototyping inside Godot or using external tools, see
   :ref:`doc_csg_tools`.


Immediate geometry
~~~~~~~~~~~~~~~~~~

Ngược lại, nếu bạn cần tạo geometry đơn giản được cập nhật thường xuyên, Godot cung cấp một resource :ref:`ImmediateMesh <class_ImmediateMesh>` đặc biệt có thể được sử dụng trong một node :ref:`MeshInstance3D <class_MeshInstance3D>`. Resource này cung cấp API immediate-mode kiểu OpenGL 1.x để tạo point, line, triangle, v.v.

2D trong 3D
~~~~~~~~~~~

Mặc dù Godot có một 2D engine mạnh mẽ, nhiều loại game sử dụng 2D trong môi trường 3D. Bằng cách sử dụng một camera cố định (orthogonal hoặc perspective) không xoay, các node như
:ref:`Sprite3D <class_Sprite3D>` and
:ref:`AnimatedSprite3D <class_AnimatedSprite3D>`
có thể được dùng để tạo các game 2D tận dụng việc kết hợp với background 3D, parallax chân thực hơn, hiệu ứng lighting/shadow, v.v.

Nhược điểm tất nhiên là độ phức tạp tăng và hiệu năng giảm so với 2D thuần túy, cũng như không còn tham chiếu trực tiếp đến việc làm việc theo pixel.

Environment
-----------

Ngoài việc chỉnh sửa scene, việc chỉnh sửa environment cũng khá phổ biến. Godot cung cấp một node :ref:`WorldEnvironment <class_WorldEnvironment>` cho phép thay đổi màu background, mode (ví dụ như đặt skybox), và áp dụng một số loại post-processing effect tích hợp sẵn. Environment cũng có thể được override trong Camera.

.. _doc_introduction_to_3d_preview_environment_light:

Preview environment và light
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, mọi scene 3D không có node :ref:`WorldEnvironment <class_WorldEnvironment>` hoặc :ref:`DirectionalLight3D <class_DirectionalLight3D>` sẽ được bật preview cho phần còn thiếu để chiếu sáng scene.

Preview light và environment chỉ hiển thị trong scene khi ở trong editor. Nếu bạn chạy scene hoặc export project, chúng sẽ không ảnh hưởng đến scene.

Có thể bật hoặc tắt preview light và environment từ menu phía trên bằng cách nhấp vào biểu tượng tương ứng của chúng.

.. image:: img/tuto_3d8.webp


Menu thả xuống có ba dấu chấm bên cạnh các biểu tượng đó có thể được dùng để điều chỉnh các thuộc tính của preview environment và light nếu chúng được bật.

.. image:: img/tuto_3d9.webp


Cùng một preview sun và environment được sử dụng cho mọi scene trong cùng một project, Vì vậy chỉ nên thực hiện những điều chỉnh áp dụng cho tất cả các scene mà bạn cần preview light và environment.

Cameras
~~~~~~~

Bất kể có bao nhiêu object được đặt trong không gian 3D, sẽ không có gì được hiển thị trừ khi một :ref:`Camera3D <class_Camera3D>` cũng được thêm vào scene. Camera có thể hoạt động với phép chiếu orthogonal hoặc perspective:

.. image:: img/tuto_3d10.webp

Camera được liên kết với (và chỉ hiển thị trong) viewport là parent hoặc grandparent của chúng. Vì gốc của scene tree là một viewport, camera sẽ hiển thị trên đó theo mặc định, nhưng nếu muốn sử dụng sub-viewport (dưới dạng render target hoặc picture-in-picture), chúng cần có các camera con riêng để hiển thị.

.. image:: img/tuto_3d11.png

Khi làm việc với nhiều camera, các quy tắc sau được áp dụng cho từng viewport:

-  Nếu không có camera nào trong scene tree, camera đầu tiên đi vào scene sẽ trở thành camera active. Các camera tiếp theo đi vào scene sẽ bị bỏ qua (trừ khi chúng được đặt là *current*). - Nếu một camera có thuộc tính "*current*", camera đó sẽ được sử dụng bất kể các camera khác trong scene. Nếu thuộc tính này được đặt, camera đó sẽ trở thành camera active và thay thế camera trước đó. - Nếu camera active rời khỏi scene tree, camera đầu tiên theo thứ tự trong tree sẽ thay thế nó.

Lights
~~~~~~

Environment background phát ra một lượng ambient light, tạo ánh sáng trên các bề mặt. Tuy nhiên, nếu không có light source nào được đặt trong scene, scene sẽ khá tối trừ khi environment background rất sáng.

Hầu hết scene ngoài trời có directional light (mặt trời hoặc mặt trăng), trong khi scene trong nhà thường có nhiều positional light (đèn, đuốc, …). Xem :ref:`doc_lights_and_shadows` để biết thêm thông tin về cách thiết lập light trong Godot.
