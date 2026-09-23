:article_outdated: Đúng

.. _doc_using_multi_mesh_instance:

Sử dụng MultiMeshInstance3D
===========================

Giới thiệu
----------

Trong trường hợp thông thường, bạn sẽ sử dụng một node :ref:`MeshInstance3D <class_MeshInstance3D>` để hiển thị một mesh 3D, chẳng hạn như mô hình nhân vật chính, nhưng trong một số trường hợp, bạn có thể muốn tạo nhiều instance của cùng một mesh trong một scene. Bạn *có thể* nhân bản cùng một node nhiều lần và điều chỉnh các transform theo cách thủ công. Đây có thể là một quy trình tẻ nhạt và kết quả có thể trông máy móc. Ngoài ra, phương pháp này không thuận tiện cho việc lặp lại nhanh chóng.
:ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>` là một trong những giải pháp có thể áp dụng cho vấn đề này.

MultiMeshInstance3D, đúng như tên gọi, tạo nhiều bản sao của một MeshInstance trên bề mặt của một mesh cụ thể. Ví dụ, bạn có thể dùng một mesh cây để phủ cây lên một mesh địa hình, với các cây có tỉ lệ và hướng ngẫu nhiên.

Thiết lập các node
------------------

Thiết lập cơ bản cần có ba node: node MultiMeshInstance3D và hai node MeshInstance3D.

Một node được dùng làm target, tức mesh bề mặt mà bạn muốn đặt nhiều mesh lên. Trong ví dụ về cây, đó sẽ là địa hình.

Node còn lại được dùng làm source, tức mesh mà bạn muốn nhân bản. Trong trường hợp cây, đó sẽ là chính cây đó.

Trong ví dụ này, chúng ta sẽ sử dụng một node :ref:`Node3D <class_Node3D>` làm node gốc của scene. Cây scene của bạn sẽ trông như sau:

.. image:: img/multimesh_scene_tree.png

.. note:: Để đơn giản, tutorial này sử dụng các primitive tích hợp sẵn.

Bây giờ bạn đã sẵn sàng mọi thứ. Chọn node MultiMeshInstance3D và xem thanh công cụ, bạn sẽ thấy một nút bổ sung có tên ``MultiMesh`` bên cạnh ``View``. Nhấp vào đó và chọn *Populate surface* trong menu thả xuống. Một cửa sổ mới có tiêu đề *Populate MultiMesh* sẽ xuất hiện.

.. image:: img/multimesh_toolbar.png

.. image:: img/multimesh_settings.png

Cài đặt MultiMesh
-----------------

Dưới đây là mô tả về các tùy chọn.

Target Surface
~~~~~~~~~~~~~~

Mesh được sử dụng làm bề mặt đích để đặt các bản sao của source mesh lên đó.

Source Mesh
~~~~~~~~~~~

Mesh mà bạn muốn nhân bản trên bề mặt đích.

Mesh Up Axis
~~~~~~~~~~~~

Trục được sử dụng làm trục hướng lên của source mesh.

Random Rotation
~~~~~~~~~~~~~~~

Ngẫu nhiên hóa phép xoay quanh trục hướng lên của source mesh.

Random Tilt
~~~~~~~~~~~

Ngẫu nhiên hóa phép xoay tổng thể của source mesh.

Random Scale
~~~~~~~~~~~~

Ngẫu nhiên hóa tỉ lệ của source mesh.

Scale
~~~~~

Tỉ lệ của source mesh sẽ được đặt trên bề mặt đích.

Amount
~~~~~~

Số lượng instance của mesh được đặt trên bề mặt đích.

Chọn bề mặt đích. Trong trường hợp cây, đây phải là node địa hình. Source mesh phải là node cây. Điều chỉnh các tham số khác theo ý muốn. Nhấn ``Populate`` và nhiều bản sao của source mesh sẽ được đặt trên target mesh. Nếu hài lòng với kết quả, bạn có thể xóa mesh instance được dùng làm source mesh.

Kết quả cuối cùng sẽ trông như sau:

.. image:: img/multimesh_result.png

Để thay đổi kết quả, hãy lặp lại các bước trước đó với những tham số khác.
