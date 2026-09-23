.. _doc_introduction_to_3d:

Giới thiệu về 3D
================

Tạo một game 3D có thể là một thử thách. Tọa độ Z bổ sung khiến nhiều kỹ thuật phổ biến từng giúp việc tạo game 2D trở nên đơn giản không còn hoạt động. Để hỗ trợ quá trình chuyển đổi này, cần lưu ý rằng Godot sử dụng các API tương tự cho 2D và 3D. Hầu hết các node đều giống nhau và có mặt ở cả phiên bản 2D lẫn 3D. Trên thực tế, bạn nên xem qua hướng dẫn về platformer 3D hoặc các hướng dẫn về nhân vật động học 3D, vì chúng gần như giống hệt các phiên bản tương ứng trong 2D.

.. figure:: img/godot-tps-demo.webp
   :align: center
   :alt: Một bản demo game 3D mẫu được tạo bằng Godot

   Bản demo Godot Third Person Shooter (TPS), có trên `Github repository <https://github.com/godotengine/tps-demo>`__ hoặc
   :ref:`Asset Library <doc_project_manager_downloading_demos>`.

Trong 3D, toán học phức tạp hơn một chút so với 2D. Để tìm hiểu phần toán liên quan dành cho các nhà phát triển game, không phải nhà toán học hay kỹ sư, hãy xem :ref:`doc_vector_math` và :ref:`doc_using_transforms`.

workspace 3D
------------

Việc chỉnh sửa các scene 3D được thực hiện trong workspace 3D. Bạn có thể chọn workspace này theo cách thủ công, nhưng nó sẽ được tự động chọn khi một node Node3D được chọn.

.. image:: img/tuto_3d3.webp

Tương tự 2D, các tab bên dưới bộ chọn workspace được dùng để chuyển đổi giữa các scene đang mở hoặc tạo scene mới bằng nút dấu cộng (+). Các dock bên trái và bên phải hẳn đã quen thuộc từ :ref:`phần giới thiệu editor <doc_editor_introduction>`.

Bên dưới bộ chọn scene là main toolbar, và bên dưới main toolbar là viewport 3D.

Main toolbar
~~~~~~~~~~~~

Một số nút trong main toolbar giống với các nút trong workspace 2D. Khi di con trỏ chuột lên một nút trong một giây, một phần giải thích ngắn cùng phím tắt sẽ được hiển thị. Một số nút có thể có chức năng bổ sung nếu nhấn thêm một phím khác. Dưới đây là phần tóm tắt chức năng chính của từng nút cùng phím tắt mặc định, theo thứ tự từ trái sang phải:

.. image:: img/3d_toolbar.webp

- **Transform Mode** (:kbd:`Q`): Bật chế độ di chuyển + xoay kết hợp cho các node đã chọn.
- **Move Mode** (:kbd:`W`): Bật chế độ di chuyển (hoặc tịnh tiến) cho các node đã chọn. Xem :ref:`doc_introduction_to_3d_space_and_manipulation` để biết thêm chi tiết.
- **Rotate Mode** (:kbd:`E`): Bật chế độ xoay cho các node đã chọn. Xem
  :ref:`doc_introduction_to_3d_space_and_manipulation` để biết thêm chi tiết.
- **Scale Mode** (:kbd:`R`): Bật chức năng scale và hiển thị các gizmo scale trên những trục khác nhau cho các node đã chọn. Xem :ref:`doc_introduction_to_3d_space_and_manipulation` để biết thêm chi tiết.
- **Select Mode** (:kbd:`V`): Cho phép chọn các node trong viewport. Nhấp chuột trái vào một node để chọn node đó. Nhấp chuột trái và kéo một hình chữ nhật sẽ chọn tất cả các node nằm trong ranh giới của hình chữ nhật khi thả chuột. Giữ :kbd:`Shift` trong khi chọn sẽ thêm các node vào vùng chọn. Nhấp vào một node đã chọn trong khi giữ :kbd:`Shift` sẽ bỏ chọn node đó. Trong chế độ này, bạn có thể dùng các gizmo để di chuyển hoặc xoay.
- **Show the list of selectable nodes at the clicked position**: Như mô tả cho thấy, tùy chọn này hiển thị danh sách các node có thể chọn tại vị trí được nhấp dưới dạng context menu, nếu có nhiều hơn một node trong khu vực được nhấp.
- **Lock** (:kbd:`Ctrl + L`) các node đã chọn, ngăn việc chọn và di chuyển chúng trong viewport. Nhấp lại vào nút này (hoặc sử dụng :kbd:`Ctrl + Shift + L`) để mở khóa các node đã chọn. Các node bị khóa chỉ có thể được chọn trong scene tree. Bạn có thể dễ dàng nhận biết chúng qua biểu tượng ổ khóa bên cạnh tên node trong scene tree. Nhấp vào biểu tượng ổ khóa này cũng sẽ mở khóa các node.
- **Group selected nodes** (:kbd:`Ctrl + G`). Tùy chọn này cho phép chọn node gốc nếu bất kỳ node con nào được chọn. Sử dụng :kbd:`Ctrl + G` để bỏ nhóm chúng. Ngoài ra, nhấp vào nút bỏ nhóm trong scene tree cũng thực hiện thao tác tương tự.
- **Ruler Mode** (:kbd:`M`): Khi được bật, bạn có thể nhấp và kéo để đo khoảng cách trong scene theo đơn vị mét.
- **Use Local Space** (:kbd:`T`): Khi được bật, các gizmo của một node được vẽ theo góc xoay của node hiện tại thay vì :ref:`global viewport axes <doc_introduction_to_3d_coordinate_system>`.
- **Use Snap** (:kbd:`Y`): Khi được bật, thao tác di chuyển và xoay sẽ snap theo lưới. Bạn cũng có thể tạm thời bật snap bằng :kbd:`Ctrl` trong khi thực hiện thao tác. Các thiết lập để thay đổi tùy chọn snap được giải thích bên dưới.
- **Use Trackball** (:kbd:`U`): Khi được bật, kéo phần trung tâm của một node (được biểu thị bằng vùng sáng đĩa tia tinh tế) sẽ xoay node giống như một trackball vật lý.
- **Preserve Children Transform** (:kbd:`P`): Khi được bật, việc transform một node sẽ giữ nguyên transform toàn cục của các node con.
- **Toggle preview sunlight**: Nếu scene không có DirectionalLight3D, bạn có thể dùng bản xem trước ánh sáng mặt trời làm nguồn sáng. Xem
  :ref:`doc_introduction_to_3d_preview_environment_light` để biết thêm chi tiết.
- **Toggle preview environment**: Nếu scene không có WorldEnvironment, bạn có thể dùng bản xem trước môi trường làm phần giữ chỗ. Xem
  :ref:`doc_introduction_to_3d_preview_environment_light` để biết thêm chi tiết.
- **Edit Sun and Environment Settings (three dots)**: Mở menu để cấu hình các thiết lập ánh sáng mặt trời và môi trường xem trước. Xem :ref:`doc_introduction_to_3d_preview_environment_light` để biết thêm chi tiết.

- **Transform menu**: Menu này có ba tùy chọn:

   - *Snap Object to Floor*: Snap một đối tượng vào một mặt sàn chắc chắn.
   - *Transform Dialog*: Mở hộp thoại để điều chỉnh thủ công các tham số transform (translate, rotate, scale và transform).
   - *Snap Settings*: Cho phép thay đổi các thiết lập snap của transform, rotate (theo độ) và scale (theo phần trăm).

- **View menu**: Điều khiển các tùy chọn chế độ xem và bật thêm các viewport:

.. image:: img/tuto_3d6.webp

Trong menu này, bạn cũng có thể hiển thị/ẩn các lưới, mặc định được đặt ở kích thước 1x1 mét, và gốc tọa độ, nơi các đường trục màu xanh dương, xanh lá cây và đỏ giao nhau. Ngoài ra, bạn có thể bật/tắt các loại gizmo cụ thể trong menu này.

.. image:: img/tuto_3d6_2.webp

Biểu tượng mắt mở nghĩa là gizmo đang hiển thị, mắt nhắm nghĩa là gizmo đang bị ẩn. Mắt mở một nửa nghĩa là gizmo cũng hiển thị xuyên qua các bề mặt đục.

Nhấp vào *Settings* trong menu view này sẽ mở một cửa sổ để thay đổi tham số *Vertical Field of View (VFOV)* (theo độ), các giá trị *Z-Near* và *Z-Far*.

Bên cạnh menu View, có thể sẽ hiển thị thêm các nút. Trong hình ảnh toolbar ở đầu chương này, một nút *Mesh* bổ sung xuất hiện vì một MeshInstance3D đang được chọn. Menu này cung cấp một số thao tác nhanh hoặc công cụ để làm việc trên một node hoặc vùng chọn cụ thể.

Menu View của viewport
~~~~~~~~~~~~~~~~~~~~~~

Bên dưới công cụ *Select*, trong viewport 3D, nhấp vào ba dấu chấm sẽ mở **View menu** của viewport. Bạn cũng có thể ẩn tất cả gizmo đang hiển thị trong chế độ xem 3D của trình chỉnh sửa thông qua menu này:

.. image:: img/tuto_3d6_1.webp

Menu này cũng hiển thị loại chế độ xem hiện tại và cho phép nhanh chóng điều chỉnh góc nhìn của viewport. Ngoài ra, menu còn cung cấp các tùy chọn để thay đổi diện mạo của các node trong viewport.

.. _doc_introduction_to_3d_coordinate_system:

Hệ tọa độ
~~~~~~~~~

Godot sử dụng hệ `metric <https://en.wikipedia.org/wiki/Metric_system>`__ cho mọi thứ trong 3D, trong đó 1 unit tương đương 1 mét. Vật lý và các lĩnh vực khác được tinh chỉnh theo tỷ lệ này. Vì vậy, cố gắng sử dụng một tỷ lệ khác thường là ý tưởng tồi (trừ khi bạn biết mình đang làm gì).

Khi làm việc với các asset 3D, tốt nhất là luôn làm việc theo đúng tỷ lệ (đặt unit thành metric trong phần mềm modeling 3D của bạn). Godot cho phép scale sau khi import và mặc dù điều này hoạt động trong hầu hết trường hợp, trong một số tình huống hiếm gặp, nó có thể gây ra các vấn đề về độ chính xác số thực (và do đó gây ra lỗi hoặc hiện tượng bất thường) ở các khu vực nhạy cảm như rendering hoặc physics. Hãy đảm bảo các artist của bạn luôn làm việc đúng tỷ lệ!

Tọa độ Y được dùng cho hướng "lên". Đối với các trục ngang X/Z, Godot sử dụng hệ tọa độ **right-handed**. Điều này có nghĩa là đối với hầu hết các object cần căn chỉnh (chẳng hạn như light hoặc camera), trục Z được dùng làm hướng "chỉ về phía trước". Quy ước này có nghĩa gần đúng rằng:

-  **X** là hai bên
-  **Y** là lên/xuống
-  **Z** là trước/sau

Xem biểu đồ này để so sánh với các phần mềm 3D khác:

.. figure:: img/introduction_to_3d_coordinate_systems.webp
   :align: center
   :alt: Biểu đồ so sánh các hệ tọa độ 3D

   Hình ảnh của `Freya Holmér <https://twitter.com/FreyaHolmer>`__


.. _doc_introduction_to_3d_space_and_manipulation:

Gizmo không gian và thao tác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc di chuyển, xoay và scale các object trong chế độ xem 3D được thực hiện thông qua các gizmo thao tác. Mỗi trục được biểu thị bằng một màu: Đỏ, Xanh lá, Xanh dương lần lượt đại diện cho X, Y, Z. Quy ước này cũng áp dụng cho grid và các gizmo khác (đồng thời áp dụng cho shader language, thứ tự các component của Vector3, Color, v.v.).

.. image:: img/tuto_3d5.webp

Một số keybinding hữu ích:

-  Để snap vị trí hoặc góc xoay, hãy nhấn :kbd:`Ctrl` trong khi di chuyển, scale hoặc xoay.
-  Để căn giữa chế độ xem vào object đã chọn, hãy nhấn :kbd:`F`.

Trong viewport, bạn có thể nhấp và giữ các mũi tên để di chuyển object theo một trục. Bạn có thể nhấp và giữ các cung để xoay object. Để khóa một trục và tự do di chuyển object theo hai trục còn lại, bạn có thể nhấp, giữ và kéo các hình chữ nhật màu.

Nếu chế độ transform được đổi từ *Select Mode* thành *Scale Mode*, các mũi tên sẽ được thay thế bằng các khối lập phương, có thể được kéo để scale một object như thể object đang được di chuyển.

Điều hướng trong môi trường 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong môi trường 3D, việc điều chỉnh góc nhìn hoặc góc mà bạn dùng để quan sát scene thường rất quan trọng. Trong Godot, có nhiều cách để điều hướng trong môi trường 3D ở viewport (hoặc spatial editor).

Các điều khiển điều hướng scene 3D mặc định tương tự Blender (nhằm duy trì một mức nhất quán nào đó trong quy trình phần mềm tự do), nhưng Editor Settings có các tùy chọn để tùy chỉnh nút chuột và hành vi sao cho tương tự các công cụ khác. Để đổi điều khiển thành điều khiển của Maya hoặc Modo, bạn có thể đi đến **Editor Settings > Editors > 3D**. Sau đó, trong *Navigation*, hãy tìm *Navigation Scheme*.

.. image:: img/tuto_3d4.webp

Với các thiết lập mặc định, các phím tắt sau đây điều khiển cách bạn điều hướng trong viewport:

Nhấn nút chuột giữa và kéo chuột cho phép bạn xoay quanh tâm của nội dung đang hiển thị trên màn hình.

Bạn cũng có thể nhấp chuột trái và giữ gizmo thao tác ở góc trên bên phải của viewport để xoay quanh tâm:

.. image:: img/tuto_3d_gizmo.webp

Nhấp chuột trái vào một trong các vòng tròn màu sẽ đặt chế độ xem thành chế độ trực giao đã chọn và menu chế độ xem của viewport sẽ được cập nhật tương ứng.

.. image:: img/tuto_3d_updated_view_menu.webp

Nếu chế độ xem *Perspective* được bật trên viewport (có thể thấy trong View menu của viewport, không phải View menu trên thanh công cụ chính), việc giữ nút chuột phải trên viewport hoặc nhấn :kbd:`Shift + F` sẽ chuyển sang chế độ "free-look". Trong chế độ này, bạn có thể di chuyển chuột để quan sát xung quanh, sử dụng :kbd:`W` :kbd:`A`
:kbd:`S` :kbd:`D` để bay quanh chế độ xem, :kbd:`E` để đi lên và :kbd:`Q` để đi xuống. Để tắt chế độ này, hãy thả nút chuột phải hoặc nhấn
:kbd:`Shift + F` lần nữa.

Trong chế độ free-look, bạn có thể tạm thời tăng tốc độ bay bằng :kbd:`Shift` hoặc giảm tốc độ bằng :kbd:`Alt`. Để thay đổi và duy trì bộ điều chỉnh tốc độ, hãy sử dụng :kbd:`mouse wheel up` hoặc :kbd:`mouse wheel down` tương ứng để tăng hoặc giảm tốc độ.

Trong chế độ trực giao, giữ nút chuột phải sẽ thay vào đó di chuyển chế độ xem. Sử dụng :kbd:`Keypad 5` để chuyển đổi giữa chế độ xem phối cảnh và trực giao.

Sử dụng phím tắt transform kiểu Blender
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.2, bạn có thể bật các phím tắt kiểu Blender để translate, rotate và scale các node. Trong Blender, các phím tắt này là:

- :kbd:`G` để translate
- :kbd:`R` để rotate
- :kbd:`S` để scale

Sau khi nhấn phím tắt trong khi viewport của 3D editor đang được focus, hãy di chuyển chuột hoặc nhập một số để di chuyển các node đã chọn theo lượng chỉ định trong các unit 3D. Bạn có thể giới hạn chuyển động vào một trục cụ thể bằng cách chỉ định trục bằng một chữ cái, sau đó nhập khoảng cách (nếu nhập giá trị bằng bàn phím).

Ví dụ, để di chuyển vùng chọn lên trên 2.5 unit, hãy nhập lần lượt chuỗi sau (Y+ là hướng lên trong Godot):

:kbd:`G`-:kbd:`Y`-:kbd:`2`-:kbd:`.`-:kbd:`5`-:kbd:`Enter`

Để sử dụng các phím tắt transform kiểu Blender trong Godot, hãy đi đến tab **Shortcuts** của Editor Settings, sau đó trong phần Spatial Editor:

- Gán **Begin Translate Transformation** cho :kbd:`G`.
- Gán **Begin Rotate Transformation** cho :kbd:`R`.
- Gán **Begin Scale Transformation** cho :kbd:`S`.
- Cuối cùng, hãy hủy gán **Scale Mode** để phím tắt của nó không xung đột với **Begin Rotate Transformation**.

nút Node3D
----------

:ref:`Node2D <class_Node2D>` là nút cơ sở cho 2D.
:ref:`Control <class_Control>` là nút cơ sở cho mọi thứ trong GUI. Theo lập luận này, engine 3D sử dụng nút :ref:`Node3D <class_Node3D>` cho mọi thứ 3D.

.. image:: img/tuto_3d1.webp

Node3D có một phép biến đổi cục bộ, tương đối so với nút cha (miễn là nút cha cũng thuộc loại **or inherits from** Node3D). Có thể truy cập phép biến đổi này dưới dạng ma trận 3×4
:ref:`Transform3D <class_Transform3D>`, hoặc dưới dạng 3 thành viên :ref:`Vector3 <class_Vector3>` biểu diễn vị trí, phép xoay Euler (các góc X, Y và Z) và tỷ lệ.

.. image:: img/tuto_3d2.webp

nội dung 3D
-----------

Không giống 2D, nơi việc tải nội dung hình ảnh và vẽ khá đơn giản, 3D phức tạp hơn một chút. Nội dung cần được tạo bằng các công cụ 3D chuyên dụng (còn gọi là công cụ Digital Content Creation, hay DCC) và xuất ra một định dạng tệp trao đổi để nhập vào Godot. Điều này là cần thiết vì các định dạng 3D không được chuẩn hóa như hình ảnh.

Mô hình được tạo thủ công (bằng phần mềm modeling 3D)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. FIXME: Needs update to properly description Godot 3.x workflow
   (used to reference a non existing doc_importing_3d_meshes importer).

Bạn có thể nhập vào Godot các mô hình 3D được tạo bằng những công cụ bên ngoài. Tùy thuộc vào định dạng, bạn có thể nhập toàn bộ scene (chính xác như trong phần mềm modeling 3D), bao gồm animation, skeletal rig, blend shape, hoặc nhập dưới dạng các resource đơn giản.

.. seealso:: Xem :ref:`doc_importing_3d_scenes` để biết thêm về việc nhập.

Hình học được tạo
~~~~~~~~~~~~~~~~~

Bạn có thể tạo hình học tùy chỉnh bằng cách sử dụng
resource :ref:`ArrayMesh <class_ArrayMesh>` trực tiếp. Chỉ cần tạo các mảng của bạn và sử dụng hàm :ref:`ArrayMesh.add_surface_from_arrays() <class_ArrayMesh_method_add_surface_from_arrays>`. Ngoài ra còn có lớp hỗ trợ :ref:`SurfaceTool <class_SurfaceTool>`, cung cấp API và các hàm hỗ trợ đơn giản hơn để lập chỉ mục, tạo normal, tangent, v.v.

Dù trong trường hợp nào, phương pháp này предназначено cho việc tạo hình học tĩnh (các mô hình không được cập nhật thường xuyên), vì việc tạo các mảng vertex và gửi chúng đến API 3D có chi phí hiệu năng đáng kể.

.. note:: Để tìm hiểu về việc tạo prototype bên trong Godot hoặc sử dụng các công cụ bên ngoài, hãy xem
   :ref:`doc_csg_tools`.


Hình học tức thời
~~~~~~~~~~~~~~~~~

Ngược lại, nếu bạn cần tạo hình học đơn giản được cập nhật thường xuyên, Godot cung cấp một resource :ref:`ImmediateMesh <class_ImmediateMesh>` đặc biệt có thể được sử dụng trong một nút :ref:`MeshInstance3D <class_MeshInstance3D>`. Resource này cung cấp API immediate mode theo phong cách OpenGL 1.x để tạo điểm, đường, tam giác, v.v.

2D trong 3D
~~~~~~~~~~~

Mặc dù Godot có một engine 2D mạnh mẽ, nhiều loại game sử dụng 2D trong môi trường 3D. Bằng cách sử dụng một camera cố định (trực giao hoặc phối cảnh) không xoay, các nút như
:ref:`Sprite3D <class_Sprite3D>` và
:ref:`AnimatedSprite3D <class_AnimatedSprite3D>` có thể được sử dụng để tạo các game 2D tận dụng sự kết hợp với nền 3D, hiệu ứng parallax chân thực hơn, hiệu ứng ánh sáng/bóng, v.v.

Tất nhiên, nhược điểm là độ phức tạp tăng lên và hiệu năng giảm so với 2D thuần túy, cũng như không còn quy chiếu làm việc theo pixel.

Môi trường
----------

Ngoài việc chỉnh sửa scene, việc chỉnh sửa môi trường cũng khá phổ biến. Godot cung cấp một nút :ref:`WorldEnvironment <class_WorldEnvironment>` cho phép thay đổi màu nền, chế độ (chẳng hạn như đặt skybox) và áp dụng một số loại hiệu ứng post-processing tích hợp sẵn. Bạn cũng có thể ghi đè môi trường trong Camera.

.. _doc_introduction_to_3d_preview_environment_light:

Môi trường và ánh sáng xem trước
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, mọi scene 3D không có nút :ref:`WorldEnvironment <class_WorldEnvironment>` hoặc :ref:`DirectionalLight3D <class_DirectionalLight3D>` sẽ được bật chế độ xem trước cho thành phần còn thiếu để chiếu sáng scene.

Ánh sáng và môi trường xem trước chỉ hiển thị trong scene khi đang ở editor. Nếu bạn chạy scene hoặc export project, chúng sẽ không ảnh hưởng đến scene.

Có thể bật hoặc tắt ánh sáng và môi trường xem trước từ menu trên cùng bằng cách nhấp vào biểu tượng tương ứng.

.. image:: img/tuto_3d8.webp


Menu thả xuống có ba dấu chấm bên cạnh các biểu tượng đó có thể được sử dụng để điều chỉnh các thuộc tính của môi trường và ánh sáng xem trước khi chúng được bật.

.. image:: img/tuto_3d9.webp


Cùng một mặt trời và môi trường xem trước được sử dụng cho mọi scene trong cùng một project, vì vậy chỉ điều chỉnh những thiết lập áp dụng cho tất cả các scene mà bạn cần ánh sáng và môi trường xem trước.

Camera
~~~~~~

Dù có bao nhiêu đối tượng được đặt trong không gian 3D, sẽ không có gì được hiển thị nếu scene không có thêm một :ref:`Camera3D <class_Camera3D>`. Camera có thể hoạt động với phép chiếu trực giao hoặc phối cảnh:

.. image:: img/tuto_3d10.webp

Camera được liên kết với viewport cha hoặc ông (và chỉ hiển thị trong viewport đó). Vì gốc của cây scene là một viewport, camera sẽ hiển thị trong đó theo mặc định; nhưng nếu muốn dùng các sub-viewport (dưới dạng render target hoặc picture-in-picture), chúng cần có các camera con riêng để hiển thị.

.. image:: img/tuto_3d11.png

Khi làm việc với nhiều camera, các quy tắc sau được áp dụng cho từng viewport:

-  Nếu trong cây scene không có camera nào, camera đầu tiên được thêm vào sẽ trở thành camera hiện hành. Các camera được thêm vào scene sau đó sẽ bị bỏ qua (trừ khi chúng được đặt là *current*).
-  Nếu một camera có thuộc tính "*current*", camera đó sẽ được sử dụng bất kể các camera khác trong scene. Khi thuộc tính này được đặt, camera đó sẽ trở thành camera hiện hành và thay thế camera trước đó.
-  Nếu một camera hiện hành rời khỏi cây scene, camera đầu tiên theo thứ tự trong cây sẽ thay thế nó.

Ánh sáng
~~~~~~~~

Môi trường nền phát ra một phần ánh sáng môi trường, ánh sáng này xuất hiện trên các bề mặt. Tuy nhiên, nếu không có nguồn sáng nào được đặt trong scene, scene sẽ khá tối, trừ khi môi trường nền rất sáng.

Hầu hết các scene ngoài trời có một directional light (mặt trời hoặc mặt trăng), trong khi scene trong nhà thường có một số positional light (đèn, đuốc, …). Xem :ref:`doc_lights_and_shadows` để biết thêm thông tin về cách thiết lập ánh sáng trong Godot.
