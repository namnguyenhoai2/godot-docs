.. _doc_retargeting_3d_skeletons:

Retarget Skeleton 3D
====================

Chia sẻ animation giữa nhiều Skeleton
-------------------------------------

Godot có các track 3D Position/Rotation/Scale (tài liệu này gọi là track "Transform") với Nodepath trỏ đến các bone để tạo animation cho bone của Skeleton. Điều này có nghĩa là bạn không thể chia sẻ animation giữa nhiều Skeleton chỉ bằng cách sử dụng cùng tên bone.

Godot cho phép mỗi bone có quan hệ cha-con, đồng thời có rotation và scale cũng như position, điều đó có nghĩa là các bone cùng tên vẫn có thể có các giá trị Transform khác nhau.

Skeleton lưu các giá trị Transform cần thiết cho pose mặc định dưới dạng Bone Rest. Nếu Bone Pose bằng Bone Rest, điều đó có nghĩa là Skeleton đang ở pose mặc định.

.. note:: Godot 3 và Godot 4 có cách hoạt động khác nhau đối với Bone Pose. Trong Godot 3, Bone Pose là tương đối so với Bone Rest, còn trong Godot 4, nó bao gồm cả Bone Rest. Xem `bài viết <https://godotengine.org/article/animation-data-redesign-40>`__ này để biết thêm thông tin.

Các model skeletal có Bone Rest khác nhau tùy thuộc vào môi trường mà chúng được export. Ví dụ, các bone của model glTF được output từ Blender có "Edit Bone Orientation" làm rotation của Bone Rest. Tuy nhiên, có những model skeletal không có rotation Bone Rest, chẳng hạn như model glTF được output từ Maya.

Để chia sẻ animation trong Godot, cần khớp cả Bone Rest lẫn Bone Name nhằm loại bỏ các track không mong muốn trong một số trường hợp. Bạn có thể thực hiện việc này bằng scene importer.

Các tùy chọn Retarget
---------------------

Bone Map
~~~~~~~~

Khi chọn node Skeleton3D trong advanced scene import menu, một menu sẽ xuất hiện ở bên phải, chứa phần "Retarget". Phần Retarget có một property duy nhất là ``bone_map``.

.. image:: img/retargeting1.webp

Khi đã chọn node Skeleton, trước tiên hãy thiết lập một :ref:`class_bonemap` mới và :ref:`class_skeletonprofile`. Godot có một preset tên là :ref:`class_skeletonprofilehumanoid` dành cho các model humanoid. Tutorial này giả định rằng bạn đang sử dụng :ref:`class_skeletonprofilehumanoid`.

.. note:: Nếu bạn cần một profile khác với :ref:`class_skeletonprofilehumanoid`, bạn có thể export một :ref:`class_skeletonprofile` từ editor bằng cách chọn Skeleton3D và sử dụng menu **Skeleton3D** trên toolbar của 3D viewport.

Khi bạn sử dụng :ref:`class_skeletonprofilehumanoid`, việc auto-mapping sẽ được thực hiện khi
:ref:`class_skeletonprofile` được thiết lập. Nếu auto-mapping không hoạt động tốt, bạn có thể map bone theo cách thủ công.

.. image:: img/retargeting2.webp

Mọi mapping bị thiếu, trùng lặp hoặc có quan hệ cha-con không chính xác sẽ được chỉ báo bằng một nút màu magenta / đỏ (tùy thuộc vào thiết lập của editor). Điều này không chặn quá trình import, nhưng cảnh báo rằng animation có thể không được chia sẻ chính xác.

.. note:: Auto-mapping sử dụng pattern matching cho tên bone. Vì vậy, chúng tôi khuyến nghị sử dụng tên tiếng Anh phổ biến cho các bone.

Sau khi thiết lập ``bone_map``, bạn có thể sử dụng một số tùy chọn trong các phần bên dưới.

.. image:: img/retargeting3.webp

Remove Tracks
~~~~~~~~~~~~~

Nếu bạn import resource dưới dạng :ref:`class_animationlibrary` sẽ được chia sẻ, chúng tôi khuyến nghị bật các tùy chọn này. Tuy nhiên, nếu bạn import resource dưới dạng scene, trong một số trường hợp nên tắt chúng. Ví dụ, nếu bạn import một nhân vật có các accessory được animate, các tùy chọn này có thể khiến accessory không được animate.

Except Bone Transform
^^^^^^^^^^^^^^^^^^^^^

Xóa mọi track ngoại trừ track bone Transform khỏi các animation.

Unimportant Positions
^^^^^^^^^^^^^^^^^^^^^

Xóa các track Position khác với ``root_bone`` và ``scale_base_bone`` được định nghĩa trong :ref:`class_skeletonprofile` khỏi các animation. Trong :ref:`class_skeletonprofilehumanoid`, điều này có nghĩa là xóa các track Position khác với "Root" và "Hips". Kể từ Godot 4, animation bao gồm Bone Rest trong giá trị Transform. Nếu bạn tắt tùy chọn này, animation có thể làm thay đổi hình dạng cơ thể theo cách không thể đoán trước.

Unmapped Bones
^^^^^^^^^^^^^^

Xóa các track bone Transform chưa được map khỏi các animation.

Bone Renamer
~~~~~~~~~~~~

Rename Bones
^^^^^^^^^^^^

Đổi tên các bone đã được map.

Unique Node
^^^^^^^^^^^

Biến Skeleton thành một node duy nhất với tên được chỉ định trong ``skeleton_name``. Điều này cho phép hợp nhất các path của animation track, không phụ thuộc vào hierarchy của scene.

Rest Fixer
~~~~~~~~~~

Các reference pose được định nghĩa trong :ref:`class_skeletonprofilehumanoid` có những quy tắc sau:

* Humanoid ở tư thế T-pose
* Humanoid hướng về +Z trong Right-Handed Y-UP Coordinate System
* Humanoid không được có Transform dưới dạng Node
* Hướng trục +Y từ joint cha đến joint con
* Rotation +X bẻ cong joint như cơ bắp đang co lại

Các quy tắc này là những định nghĩa thuận tiện cho blend animation và Inverse Kinematics (IK). Nếu model của bạn không khớp với định nghĩa này, bạn cần sửa model bằng các tùy chọn này.

Apply Node Transform
^^^^^^^^^^^^^^^^^^^^

Nếu asset không được export chính xác để chia sẻ, Skeleton được import có thể có Transform dưới dạng Node. Ví dụ, glTF được export từ Blender mà không thực hiện "Apply Transform" là một trường hợp như vậy. Model trông có vẻ khớp với định nghĩa, nhưng các Transform nội bộ lại khác với định nghĩa. Tùy chọn này sửa các model như vậy bằng cách apply Transform khi import.

.. note:: Nếu scene được import chứa các object khác ngoài Skeleton, tùy chọn này có thể gây ảnh hưởng tiêu cực.

Normalize Position Tracks
^^^^^^^^^^^^^^^^^^^^^^^^^

Track Position chủ yếu được dùng để di chuyển model, nhưng việc chia sẻ animation chuyển động giữa các model có chiều cao khác nhau có thể tạo ra cảm giác trượt do khác biệt về độ dài bước chân. Tùy chọn này chuẩn hóa các giá trị của track Position dựa trên chiều cao ``scale_base_bone``. Chiều cao ``scale_base_bone`` được lưu trong Skeleton dưới dạng ``motion_scale``, và các giá trị track Position đã chuẩn hóa sẽ được nhân với giá trị đó khi playback. Nếu tắt tùy chọn này, các track Position sẽ không được chuẩn hóa và ``motion_scale`` của Skeleton luôn được import dưới dạng ``1.0``.

Với :ref:`class_skeletonprofilehumanoid`, ``scale_base_bone`` là "Hips", do đó chiều cao của Hips được sử dụng làm ``motion_scale``.

Overwrite Axis
^^^^^^^^^^^^^^

Hợp nhất Bone Rest của các model bằng cách ghi đè chúng để khớp với các reference pose được định nghĩa trong :ref:`class_skeletonprofile`.

.. note:: Đây là tùy chọn quan trọng nhất để chia sẻ animation trong Godot 4, nhưng hãy lưu ý rằng tùy chọn này có thể tạo ra kết quả rất tệ **nếu Bone Rest gốc được thiết lập bên ngoài là quan trọng**. Nếu muốn chia sẻ animation mà vẫn giữ Bone Rest gốc, hãy cân nhắc sử dụng `Realtime Retarget Module <https://github.com/TokageItLab/realtime_retarget>`__.

Fix Silhouette
^^^^^^^^^^^^^^

Cố gắng làm cho hình dáng của model khớp với hình dáng của các tư thế tham chiếu được xác định trong :ref:`class_skeletonprofile`, chẳng hạn như T-Pose. Tùy chọn này không thể khắc phục các hình dáng khác biệt quá nhiều và có thể không hiệu quả trong việc khắc phục bone roll.

Với :ref:`class_skeletonprofilehumanoid`, bạn không cần bật tùy chọn này cho các model ở tư thế T-pose, nhưng nên bật cho các model ở tư thế A-pose. Tuy nhiên, trong trường hợp đó, kết quả cố định bàn chân có thể không tốt tùy thuộc vào độ cao của gót chân model, vì vậy có thể cần thêm tên các bone mà bạn không muốn cố định vào mảng ``filter`` trong :ref:`class_skeletonprofile`, như trong ví dụ bên dưới.

.. image:: img/retargeting4.webp

Ngoài ra, đối với các model có đầu gối hoặc bàn chân bị cong, có thể cần điều chỉnh độ cao của ``scale_base_bone``. Bạn có thể sử dụng tùy chọn ``base_height_adjustment`` cho việc đó.
