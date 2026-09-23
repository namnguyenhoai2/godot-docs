.. _doc_importing_3d_scenes_model_export_considerations:

Các lưu ý khi export model
==========================

Trước khi export model 3D từ một ứng dụng tạo model 3D, chẳng hạn như Blender, có một số điều cần lưu ý để đảm bảo model tuân theo các quy ước và best practice dành cho Godot.

Quy ước hướng của asset 3D
--------------------------

Godot sử dụng hệ tọa độ thuận tay phải, với Y là trục hướng lên và trục -Z là hướng tiến của camera. Đây cũng là quy ước của OpenGL. Điều này có nghĩa là +Z hướng ra sau, +X hướng sang phải và -X hướng sang trái đối với camera.

Quy ước đối với asset 3D là hướng mặt về phía đối diện với camera, để các nhân vật và asset khác mặc định hướng về phía camera. Quy ước này cực kỳ phổ biến trong các ứng dụng tạo model 3D và được `chuẩn hóa trong glTF như một phần của đặc tả glTF 2.0 <https://registry.khronos.org/glTF/specs/2.0/glTF-2.0.html#coordinate-system-and-units>`__. Điều này có nghĩa là đối với các asset 3D có hướng (chẳng hạn như nhân vật), trục +Z là hướng phía trước, vì vậy -Z là phía sau, +X là bên trái và -X là bên phải của asset 3D. Trong Blender, điều này có nghĩa là +Y là phía sau và -Y là phía trước của asset.

Khi xoay một asset 3D có hướng trong Godot, hãy sử dụng ``use_model_front`` tùy chọn trên các hàm ``look_at`` và sử dụng các hằng số ``Vector3.MODEL_*`` để thực hiện phép tính trong không gian cục bộ của asset có hướng.

Đối với các asset không có mặt trước hoặc hướng tiến cố định, chẳng hạn như bản đồ game hoặc địa hình, hãy thay vào đó chú ý đến các hướng chính. Quy ước trong Godot và đại đa số các ứng dụng khác là +X hướng đông và -X hướng tây. Do hệ tọa độ thuận tay phải với Y là trục hướng lên của Godot, điều này có nghĩa là +Z hướng nam và -Z hướng bắc. Trong Blender, điều này có nghĩa là +Y hướng bắc và -Y hướng nam.

Export texture riêng biệt
-------------------------

Mặc dù texture có thể được export cùng với model trong một số định dạng tệp nhất định, chẳng hạn như glTF 2.0, bạn cũng có thể export chúng riêng biệt. Godot sử dụng PBR (physically based rendering) cho material, vì vậy nếu một chương trình tạo texture có thể export texture PBR thì chúng có thể hoạt động trong Godot. Các chương trình này bao gồm `bộ công cụ Substance <https://www.adobe.com/creativecloud/3d-ar.html>`__, `ArmorPaint (mã nguồn mở) <https://armorpaint.org/>`__ và `Material Maker (mã nguồn mở) <https://github.com/RodZill4/material-maker>`__.

.. seealso::

    Để biết thêm thông tin về material của Godot, hãy xem :ref:`doc_standard_material_3d`.

Các lưu ý khi export
--------------------

Vì GPU chỉ có thể render các triangle, các mesh chứa quad hoặc N-gon phải được *triangulate* trước khi có thể render. Godot có thể triangulate mesh khi import, nhưng kết quả có thể không ổn định hoặc không chính xác, đặc biệt với N-gon. Bất kể ứng dụng đích là gì, việc triangulate *trước khi* export scene sẽ cho kết quả nhất quán hơn và nên được thực hiện bất cứ khi nào có thể.

Để tránh các vấn đề do triangulate không chính xác sau khi import vào Godot, bạn nên để phần mềm tạo model 3D tự triangulate các object. Trong Blender, bạn có thể thực hiện việc này bằng cách thêm modifier Triangulate vào các object và đảm bảo rằng **Apply Modifiers** được chọn trong hộp thoại export. Ngoài ra, tùy thuộc vào exporter, bạn có thể tìm và bật tùy chọn **Triangulate Faces** trong hộp thoại export.

Để tránh các vấn đề khi chọn 3D trong editor, bạn nên apply transform của object trong phần mềm tạo model 3D trước khi export scene.

.. note::

    Điều quan trọng là mesh không bị biến dạng bởi bone khi export. Hãy đảm bảo skeleton được đưa về T-pose hoặc rest pose mặc định trước khi export bằng trình chỉnh sửa 3D ưa thích của bạn.

Các lưu ý về lighting
---------------------

Mặc dù có thể import light từ một scene 3D bằng định dạng glTF, ``.blend`` hoặc Collada, nhìn chung bạn nên thiết kế lighting của scene trong Godot editor sau khi import scene.

Điều này cho phép bạn cảm nhận chính xác hơn về kết quả cuối cùng, vì các engine khác nhau sẽ render light theo những cách khác nhau. Điều này cũng tránh các vấn đề khiến light trở nên quá mạnh hoặc quá mờ do quá trình import.
