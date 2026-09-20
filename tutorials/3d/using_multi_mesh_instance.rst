:article_outdated: True

.. _doc_using_multi_mesh_instance:

Sử dụng MultiMeshInstance3D
===========================

Giới thiệu
----------

Trong trường hợp thông thường, bạn sẽ sử dụng một node :ref:`MeshInstance3D <class_MeshInstance3D>` để hiển thị một 3D mesh, chẳng hạn như mô hình nhân vật chính, nhưng trong một số trường hợp, bạn sẽ muốn tạo nhiều instance của cùng một mesh trong một scene. Bạn *có thể* nhân bản cùng một node nhiều lần và điều chỉnh các transform theo cách thủ công. Đây có thể là một quy trình tẻ nhạt và kết quả có thể trông máy móc. Ngoài ra, phương pháp này không thuận tiện cho việc lặp lại nhanh.
:ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>` is one of the possible
các giải pháp cho vấn đề này.

MultiMeshInstance3D, đúng như tên gọi, tạo nhiều bản sao của một MeshInstance trên bề mặt của một mesh cụ thể. Ví dụ, bạn có thể dùng một tree mesh để phủ một landscape mesh bằng các cây có scale và hướng ngẫu nhiên.

Thiết lập các node
------------------

Thiết lập cơ bản cần ba node: node MultiMeshInstance3D và hai node MeshInstance3D.

Một node được dùng làm target, tức surface mesh mà bạn muốn đặt nhiều mesh lên. Trong ví dụ về cây, đây sẽ là landscape.

Node còn lại được dùng làm source, tức mesh mà bạn muốn nhân bản. Trong trường hợp cây, đây sẽ là chính cây đó.

Trong ví dụ này, chúng ta sẽ dùng một node :ref:`Node3D <class_Node3D>` làm root node của scene. Cây scene của bạn sẽ trông như sau:

.. image:: img/multimesh_scene_tree.png

.. note:: For simplicity's sake, this tutorial uses built-in primitives.

Bây giờ bạn đã sẵn sàng mọi thứ. Chọn node MultiMeshInstance3D và quan sát toolbar, bạn sẽ thấy một nút bổ sung có tên ``MultiMesh`` bên cạnh ``View``. Nhấp vào đó và chọn *Populate surface* trong menu thả xuống. Một cửa sổ mới có tiêu đề *Populate MultiMesh* sẽ xuất hiện.

.. image:: img/multimesh_toolbar.png

.. image:: img/multimesh_settings.png

Các thiết lập MultiMesh
-----------------------

Dưới đây là mô tả về các tùy chọn.

Target Surface
~~~~~~~~~~~~~~

Mesh được dùng làm surface target để đặt các bản sao của source mesh lên đó.

Source Mesh
~~~~~~~~~~~

Mesh mà bạn muốn nhân bản trên target surface.

Mesh Up Axis
~~~~~~~~~~~~

Trục được dùng làm up axis của source mesh.

Random Rotation
~~~~~~~~~~~~~~~

Ngẫu nhiên hóa rotation quanh up axis của source mesh.

Random Tilt
~~~~~~~~~~~

Ngẫu nhiên hóa rotation tổng thể của source mesh.

Random Scale
~~~~~~~~~~~~

Ngẫu nhiên hóa scale của source mesh.

Scale
~~~~~

Scale của source mesh sẽ được đặt trên target surface.

Amount
~~~~~~

Số lượng mesh instance được đặt trên target surface.

Chọn target surface. Trong trường hợp cây, đây phải là node landscape. Source mesh phải là node tree. Điều chỉnh các tham số còn lại theo tùy chọn của bạn. Nhấn ``Populate`` và nhiều bản sao của source mesh sẽ được đặt trên target mesh. Nếu hài lòng với kết quả, bạn có thể xóa mesh instance được dùng làm source mesh.

Kết quả cuối cùng sẽ trông như sau:

.. image:: img/multimesh_result.png

Để thay đổi kết quả, hãy lặp lại các bước trước đó với những tham số khác.
