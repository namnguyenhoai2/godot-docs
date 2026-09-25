.. _doc_advanced_physics_interpolation:

Nội suy vật lý nâng cao
=======================

Mặc dù các hướng dẫn trước đó sẽ cho kết quả đạt yêu cầu trong nhiều game, nhưng trong một số trường hợp, bạn sẽ muốn tiến thêm một bước để đạt được kết quả tốt nhất có thể và trải nghiệm mượt mà nhất có thể.

Các ngoại lệ đối với nội suy vật lý tự động
-------------------------------------------

Ngay cả khi nội suy vật lý đang được bật, vẫn có thể có một số tình huống cục bộ mà bạn sẽ muốn tắt nội suy tự động cho một
:ref:`Node<class_Node>` (hoặc một nhánh của :ref:`SceneTree<class_SceneTree>`), và có quyền kiểm soát chi tiết hơn bằng cách thực hiện nội suy thủ công.

Bạn có thể thực hiện việc này bằng thuộc tính :ref:`Node.physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`, thuộc tính này có trong tất cả các Node. Ví dụ, nếu bạn tắt nội suy cho một Node, các node con cũng sẽ bị ảnh hưởng đệ quy (vì mặc định chúng kế thừa thiết lập của node cha). Điều này có nghĩa là bạn có thể dễ dàng tắt nội suy cho toàn bộ một subscene.

.. figure:: img/physics_interpolation_mode.webp

Đáng lưu ý là, cả trong 2D và 3D, nội suy vật lý được thực hiện trên **biến đổi cục bộ** của mỗi instance. Trong quá trình render, các biến đổi cục bộ đã nội suy được truyền xuống các node con.

Điều này có nghĩa là nếu một node cha có ``physics_interpolation_mode`` được đặt thành ``On``, nhưng node con được đặt thành ``Off``, node con vẫn sẽ được nội suy nếu node cha đang di chuyển. *Chỉ biến đổi cục bộ của node con là không được nội suy.* Vì vậy, việc kiểm soát trạng thái bật / tắt của các node cần được cân nhắc và lên kế hoạch.

Tình huống phổ biến nhất mà bạn có thể muốn tự thực hiện nội suy là với Cameras.

Cameras
~~~~~~~

Trong nhiều trường hợp, một :ref:`Camera3D<class_Camera3D>` có thể sử dụng nội suy tự động giống như mọi node khác. Tuy nhiên, để đạt kết quả tốt nhất, đặc biệt ở tốc độ tick vật lý thấp, bạn nên áp dụng cách tiếp cận thủ công cho việc nội suy camera.

Điều này là vì người xem rất nhạy cảm với chuyển động của camera. Chẳng hạn, một Camera3D được căn chỉnh lại đôi chút sau mỗi 1/10 giây (ở tốc độ tick 10tps) thường sẽ dễ nhận thấy. Bạn có thể đạt được kết quả mượt mà hơn nhiều bằng cách di chuyển camera trong ``_process`` ở mỗi frame và tự theo dõi một target đã được nội suy.

Nội suy camera thủ công
~~~~~~~~~~~~~~~~~~~~~~~

Đảm bảo camera sử dụng không gian tọa độ toàn cục
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bước đầu tiên khi thực hiện nội suy camera thủ công là đảm bảo transform của Camera3D được chỉ định trong *không gian toàn cục* thay vì kế thừa transform của một node cha đang di chuyển. Điều này là vì có thể xảy ra phản hồi giữa chuyển động của node cha của Camera3D và chuyển động của chính Node camera, làm hỏng việc nội suy.

Có hai cách để thực hiện việc này:

1) Di chuyển Camera3D để nó độc lập trên nhánh riêng, thay vì là node con của một đối tượng đang di chuyển.

.. image:: img/fti_camera_worldspace.webp

2) Gọi :ref:`Node3D.top_level<class_Node3D_property_top_level>` và đặt giá trị này thành ``true``, thao tác này sẽ khiến Camera bỏ qua transform của node cha.

Ví dụ điển hình
^^^^^^^^^^^^^^^

Một ví dụ điển hình về cách tiếp cận tùy chỉnh là sử dụng hàm ``look_at`` trong Camera3D ở mỗi frame trong ``_process()`` để hướng về một node target (chẳng hạn như người chơi).

Nhưng có một vấn đề. Nếu chúng ta sử dụng ``get_global_transform()`` truyền thống trên một node "target" của Camera3D, transform này sẽ chỉ hướng Camera3D vào target *tại tick vật lý hiện tại*. Đây *không* phải điều chúng ta muốn, vì camera sẽ giật theo mỗi tick vật lý khi target di chuyển. Mặc dù camera có thể được cập nhật ở mỗi frame, điều này không giúp chuyển động mượt mà nếu *target* chỉ thay đổi ở mỗi tick vật lý.

get_global_transform_interpolated()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Điều chúng ta thực sự muốn camera hướng tới không phải là vị trí của target tại tick vật lý, mà là vị trí *đã nội suy*, tức vị trí mà target sẽ được render.

Chúng ta có thể thực hiện việc này bằng hàm :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`. Hàm này hoạt động chính xác như khi lấy :ref:`Node3D.global_transform<class_Node3D_property_global_transform>`, nhưng cung cấp cho bạn transform *đã nội suy* (trong một lần gọi ``_process()``).

.. important:: ``get_global_transform_interpolated()`` chỉ nên được sử dụng một hoặc hai lần cho các trường hợp đặc biệt như camera. Bạn **không** nên sử dụng nó ở khắp nơi trong code (vì cả lý do hiệu năng lẫn để đảm bảo gameplay chính xác).

.. note:: Ngoài các ngoại lệ như camera, trong hầu hết trường hợp, game logic của bạn nên nằm trong ``_physics_process()``. Trong game logic, bạn nên gọi ``get_global_transform()`` hoặc ``get_transform()``, các hàm này sẽ cung cấp transform vật lý hiện tại (lần lượt trong không gian toàn cục hoặc cục bộ), thường là điều bạn cần cho code gameplay.

Ví dụ script camera thủ công
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dưới đây là ví dụ về một camera cố định đơn giản theo dõi một target đã được nội suy:

.. code-block:: gdscript

    extends Camera3D

    # Node mà camera sẽ theo dõi
    var _target

    # Chúng ta sẽ lerp mượt mà để theo dõi target
    # thay vì theo dõi chính xác
    var _target_pos : Vector3 = Vector3()

    func _ready() -> void:
        # Tìm node target
        _target = get_node("../Player")

        # Tắt nội suy vật lý tự động cho Camera3D,
        # chúng ta sẽ thực hiện việc này thủ công
        set_physics_interpolation_mode(Node.PHYSICS_INTERPOLATION_MODE_OFF)

    func _process(delta: float) -> void:
        # Tìm transform đã nội suy hiện tại của target
        var tr : Transform = _target.get_global_transform_interpolated()

        # Cung cấp thao tác lerp mượt mà có độ trễ hướng tới vị trí của target
        _target_pos = lerp(_target_pos, tr.origin, min(delta, 1.0))

        # Vị trí camera cố định, nhưng camera sẽ theo dõi target
        look_at(_target_pos, Vector3(0, 1, 0))

Điều khiển bằng chuột
^^^^^^^^^^^^^^^^^^^^^

Điều khiển bằng chuột là một cách rất phổ biến để điều khiển camera. Nhưng có một vấn đề. Không giống như input bàn phím, vốn có thể được lấy mẫu định kỳ ở tick vật lý, các sự kiện di chuyển chuột có thể đến liên tục. Camera được kỳ vọng sẽ phản ứng và theo dõi các chuyển động chuột này ở frame tiếp theo, thay vì chờ đến tick vật lý tiếp theo.

Trong tình huống này, tốt hơn hết là tắt nội suy vật lý cho node camera (bằng cách sử dụng :ref:`Node.physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`) và áp dụng trực tiếp input chuột vào rotation của camera, thay vì áp dụng nó trong ``_physics_process``.

Đôi khi, đặc biệt với camera, bạn sẽ muốn sử dụng kết hợp giữa nội suy và không nội suy:

- Camera góc nhìn thứ nhất có thể đặt camera tại vị trí của người chơi (có thể bằng cách sử dụng
  :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`), nhưng điều khiển phép xoay Camera từ mouse look *without* nội suy.
- Camera góc nhìn thứ ba cũng có thể xác định điểm nhìn (vị trí mục tiêu) của camera bằng cách sử dụng
  :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`, nhưng đặt camera bằng mouse look *without* nội suy.

Có nhiều cách kết hợp và biến thể của các loại camera, nhưng cần hiểu rằng trong nhiều trường hợp, việc tắt nội suy vật lý tự động và tự xử lý nội suy có thể cho kết quả tốt hơn.

Tắt nội suy trên các node khác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù camera là ví dụ phổ biến nhất, có một số trường hợp bạn có thể muốn các node khác tự kiểm soát nội suy của chúng hoặc không được nội suy. Ví dụ, hãy xét một người chơi trong game góc nhìn từ trên xuống, với phép xoay được điều khiển bằng mouse look. Việc tắt phép xoay vật lý cho phép phép xoay của người chơi khớp với chuột theo thời gian thực.


MultiMeshes
~~~~~~~~~~~

Mặc dù hầu hết các Node trực quan tuân theo mô hình một Node, một phiên bản trực quan, MultiMeshes có thể điều khiển nhiều phiên bản từ cùng một Node. Do đó, chúng có thêm một số hàm để điều khiển chức năng nội suy theo cơ sở *per-instance*. Bạn nên tìm hiểu các hàm này nếu đang sử dụng MultiMeshes được nội suy.

- :ref:`MultiMesh.reset_instance_physics_interpolation<class_MultiMesh_method_reset_instance_physics_interpolation>`
- :ref:`MultiMesh.set_buffer_interpolated<class_MultiMesh_method_set_buffer_interpolated>`

Thông tin đầy đủ có trong :ref:`MultiMesh<class_MultiMesh>` tài liệu.
