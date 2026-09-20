.. _doc_advanced_physics_interpolation:

Nội suy vật lý nâng cao
=======================

Mặc dù các hướng dẫn trước sẽ cho kết quả thỏa đáng trong nhiều trò chơi, nhưng trong một số trường hợp, bạn sẽ muốn tiến thêm một bước để đạt được kết quả tốt nhất có thể và trải nghiệm mượt mà nhất có thể.

Các trường hợp ngoại lệ đối với nội suy vật lý tự động
------------------------------------------------------

Ngay cả khi nội suy vật lý đang được bật, vẫn có thể có một số tình huống cục bộ mà trong đó bạn sẽ có lợi nếu tắt nội suy tự động cho một
:ref:`Node<class_Node>` (or branch of the :ref:`SceneTree<class_SceneTree>`), and
có quyền kiểm soát tinh vi hơn bằng cách thực hiện nội suy thủ công.

Bạn có thể thực hiện việc này bằng thuộc tính :ref:`Node.physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`, thuộc tính này có trong mọi Node. Ví dụ, nếu bạn tắt nội suy cho một Node, các node con cũng sẽ bị ảnh hưởng theo cách đệ quy (vì mặc định chúng kế thừa thiết lập của node cha). Điều này có nghĩa là bạn có thể dễ dàng tắt nội suy cho toàn bộ một subscene.

.. figure:: img/physics_interpolation_mode.webp

Đáng lưu ý là trong cả 2D và 3D, nội suy vật lý được thực hiện trên **biến đổi cục bộ** của từng instance. Trong quá trình render, các biến đổi cục bộ đã nội suy được truyền xuống các node con.

Điều này có nghĩa là nếu một node cha được đặt ``physics_interpolation_mode`` thành ``On``, nhưng node con được đặt thành ``Off``, node con vẫn sẽ được nội suy nếu node cha đang di chuyển. *Chỉ biến đổi cục bộ của node con là không được nội suy.* Vì vậy, việc kiểm soát trạng thái bật / tắt của các node cần được cân nhắc và lên kế hoạch.

Tình huống phổ biến nhất mà bạn có thể muốn tự thực hiện nội suy là với Camera.

Camera
~~~~~~

Trong nhiều trường hợp, một :ref:`Camera3D<class_Camera3D>` có thể sử dụng nội suy tự động giống như bất kỳ node nào khác. Tuy nhiên, để đạt kết quả tốt nhất, đặc biệt ở tốc độ tick vật lý thấp, bạn nên áp dụng cách tiếp cận thủ công đối với nội suy camera.

Lý do là người xem rất nhạy với chuyển động của camera. Chẳng hạn, một Camera3D căn chỉnh lại một chút sau mỗi 1/10 giây (ở tốc độ tick 10tps) thường sẽ dễ nhận thấy. Bạn có thể đạt được kết quả mượt mà hơn nhiều bằng cách di chuyển camera trong mỗi frame ở ``_process``, rồi tự mình theo dõi một target đã được nội suy.

Nội suy camera thủ công
~~~~~~~~~~~~~~~~~~~~~~~

Đảm bảo camera sử dụng không gian tọa độ global
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bước đầu tiên khi thực hiện nội suy camera thủ công là đảm bảo biến đổi của Camera3D được xác định trong *global space* thay vì kế thừa biến đổi của một node cha đang di chuyển. Lý do là có thể xảy ra phản hồi giữa chuyển động của node cha của Camera3D và chuyển động của chính Camera, làm ảnh hưởng đến nội suy.

Có hai cách để thực hiện việc này:

1) Di chuyển Camera3D để nó độc lập trên nhánh riêng, thay vì là node con của một đối tượng đang di chuyển.

.. image:: img/fti_camera_worldspace.webp

2) Gọi :ref:`Node3D.top_level<class_Node3D_property_top_level>` và đặt giá trị này thành ``true``, thao tác này sẽ khiến Camera bỏ qua biến đổi của node cha.

Ví dụ điển hình
^^^^^^^^^^^^^^^

Một ví dụ điển hình về cách tiếp cận tùy chỉnh là sử dụng hàm ``look_at`` trong Camera3D ở mỗi frame trong ``_process()`` để hướng về một node target (chẳng hạn như người chơi).

Nhưng có một vấn đề. Nếu chúng ta sử dụng ``get_global_transform()`` truyền thống trên node "target" của Camera3D, biến đổi này sẽ chỉ khiến Camera3D tập trung vào target *tại tick vật lý hiện tại*. Đây *không phải* điều chúng ta muốn, vì camera sẽ nhảy mỗi tick vật lý khi target di chuyển. Mặc dù camera có thể được cập nhật ở mỗi frame, điều này không giúp tạo ra chuyển động mượt mà nếu *target* chỉ thay đổi ở mỗi tick vật lý.

get_global_transform_interpolated()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Điều chúng ta thực sự muốn camera tập trung vào không phải là vị trí của target tại tick vật lý, mà là vị trí đã được *nội suy*, tức vị trí mà target sẽ được render.

Chúng ta có thể thực hiện việc này bằng hàm :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`. Hàm này hoạt động chính xác như khi lấy :ref:`Node3D.global_transform<class_Node3D_property_global_transform>`, nhưng cung cấp cho bạn biến đổi đã được *nội suy* (trong một lệnh gọi ``_process()``).

.. important:: ``get_global_transform_interpolated()`` should only be used once or
               hai lần cho các trường hợp đặc biệt như camera. Không nên sử dụng nó **ở khắp nơi** trong code của bạn (cả vì lý do hiệu năng lẫn để đảm bảo gameplay chính xác).

.. note:: Aside from exceptions like the camera, in most cases, your game logic
          nên nằm trong ``_physics_process()``. Trong logic trò chơi, bạn nên gọi ``get_global_transform()`` hoặc ``get_transform()``, các hàm này sẽ cung cấp biến đổi vật lý hiện tại (lần lượt trong không gian global hoặc local), đây thường là điều bạn sẽ muốn dùng trong code gameplay.

Script camera thủ công mẫu
^^^^^^^^^^^^^^^^^^^^^^^^^^

Dưới đây là một ví dụ về camera cố định đơn giản theo dõi một target đã được nội suy:

.. code-block:: gdscript

    extends Camera3D

    # Node mà camera sẽ theo dõi
    var _target

    # Chúng ta sẽ dùng lerp mượt mà để theo dõi target
    # thay vì bám theo chính xác
    var _target_pos : Vector3 = Vector3()

    func _ready() -> void:
        # Tìm node target
        _target = get_node("../Player")

        # Tắt nội suy vật lý tự động cho Camera3D,
        # chúng ta sẽ thực hiện việc này thủ công
        set_physics_interpolation_mode(Node.PHYSICS_INTERPOLATION_MODE_OFF)

    func _process(delta: float) -> void:
        # Tìm biến đổi đã nội suy hiện tại của target
        var tr : Transform = _target.get_global_transform_interpolated()

        # Tạo hiệu ứng lerp mượt mà có độ trễ hướng đến vị trí của target
        _target_pos = lerp(_target_pos, tr.origin, min(delta, 1.0))

        # Vị trí camera cố định, nhưng camera sẽ theo dõi target
        look_at(_target_pos, Vector3(0, 1, 0))

Mouse look
^^^^^^^^^^

Mouse look là một cách điều khiển camera rất phổ biến. Nhưng có một vấn đề. Không giống input từ bàn phím, vốn có thể được lấy mẫu định kỳ ở tick vật lý, các sự kiện di chuyển chuột có thể đến liên tục. Camera được kỳ vọng sẽ phản ứng và theo dõi những chuyển động chuột này ở frame tiếp theo, thay vì chờ đến tick vật lý tiếp theo.

Trong tình huống này, tốt hơn là tắt nội suy vật lý cho node camera (bằng :ref:`Node.physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`) và áp dụng trực tiếp input chuột vào rotation của camera, thay vì áp dụng nó trong ``_physics_process``.

Đôi khi, đặc biệt với camera, bạn sẽ muốn sử dụng kết hợp cả nội suy và không nội suy:

- Camera góc nhìn thứ nhất có thể đặt camera tại vị trí của người chơi (có thể sử dụng
  :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`),
  nhưng điều khiển rotation của Camera bằng mouse look *mà không* nội suy. - Camera góc nhìn thứ ba cũng có thể xác định hướng nhìn (vị trí target) của camera bằng cách sử dụng
  :ref:`Node3D.get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`,
  nhưng đặt vị trí camera bằng mouse look *mà không* nội suy.

Có rất nhiều biến thể và cách kết hợp của các loại camera, nhưng rõ ràng là trong nhiều trường hợp, việc tắt nội suy vật lý tự động và tự xử lý có thể mang lại kết quả tốt hơn.

Tắt nội suy trên các node khác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù camera là ví dụ phổ biến nhất, vẫn có một số trường hợp bạn có thể muốn các node khác tự kiểm soát nội suy của chúng hoặc không được nội suy. Ví dụ, hãy xét một người chơi trong trò chơi góc nhìn từ trên xuống, với rotation được điều khiển bằng mouse look. Việc tắt nội suy rotation vật lý cho phép rotation của người chơi khớp với chuột theo thời gian thực.


MultiMeshes
~~~~~~~~~~~

Mặc dù hầu hết các Node trực quan tuân theo mô hình một Node, một instance trực quan, MultiMeshes có thể điều khiển nhiều instance từ cùng một Node. Vì vậy, chúng có thêm một số hàm để kiểm soát chức năng nội suy theo cơ sở *từng instance*. Bạn nên tìm hiểu các hàm này nếu đang sử dụng MultiMeshes đã được nội suy.

- :ref:`MultiMesh.reset_instance_physics_interpolation<class_MultiMesh_method_reset_instance_physics_interpolation>` - :ref:`MultiMesh.set_buffer_interpolated<class_MultiMesh_method_set_buffer_interpolated>`

Thông tin đầy đủ có trong tài liệu :ref:`MultiMesh<class_MultiMesh>`.
