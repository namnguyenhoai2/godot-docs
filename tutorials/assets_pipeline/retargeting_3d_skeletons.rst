.. _doc_retargeting_3d_skeletons:

Retarget Skeleton 3D
====================

Để chia sẻ animation giữa nhiều Skeleton
----------------------------------------

Godot có các track Position/Rotation/Scale 3D (mà tài liệu này gọi là track "Transform") với Nodepath trỏ đến các bone để tạo animation cho bone của Skeleton. Điều này có nghĩa là bạn không thể chia sẻ animation giữa nhiều Skeleton chỉ bằng cách sử dụng cùng tên bone.

Godot cho phép mỗi bone có quan hệ cha-con và có rotation, scale cũng như position, điều này có nghĩa là các bone cùng tên vẫn có thể có các giá trị Transform khác nhau.

Skeleton lưu trữ các giá trị Transform cần thiết cho pose mặc định dưới dạng Bone Rest. Nếu Bone Pose bằng Bone Rest, điều đó có nghĩa là Skeleton đang ở pose mặc định.

.. note:: Godot 3 and Godot 4 have different Bone Pose behaviors.
          Trong Godot 3, Bone Pose là tương đối so với Bone Rest, nhưng trong Godot 4, nó bao gồm cả Bone Rest. Xem `article <https://godotengine.org/article/animation-data-redesign-40>`__ để biết thêm thông tin.

Các model skeletal có Bone Rest khác nhau tùy thuộc vào môi trường mà chúng được export. Ví dụ, các bone của model glTF được output từ Blender có "Edit Bone Orientation" làm rotation của Bone Rest. Tuy nhiên, có những model skeletal không có rotation Bone Rest, chẳng hạn như model glTF được output từ Maya.

Để chia sẻ animation trong Godot, cần khớp cả Bone Rest lẫn Bone Name nhằm loại bỏ các track không mong muốn trong một số trường hợp. Bạn có thể thực hiện việc này bằng scene importer.

Các tùy chọn cho Retargeting
----------------------------

Bone Map
~~~~~~~~

Khi bạn chọn node Skeleton3D trong advanced scene import menu, một menu sẽ xuất hiện ở phía bên phải, chứa section "Retarget". Section Retarget có một property duy nhất ``bone_map``.

.. image:: img/retargeting1.webp

Khi đã chọn node Skeleton, trước tiên hãy thiết lập một :ref:`class_bonemap` mới và :ref:`class_skeletonprofile`. Godot có một preset tên là :ref:`class_skeletonprofilehumanoid` dành cho các model humanoid. Tutorial này tiếp tục với giả định rằng bạn đang sử dụng :ref:`class_skeletonprofilehumanoid`.

.. note:: If you need a profile that is different from :ref:`class_skeletonprofilehumanoid`, you can export
          một :ref:`class_skeletonprofile` từ editor bằng cách chọn Skeleton3D và sử dụng menu **Skeleton3D** trên toolbar của viewport 3D.

Khi bạn sử dụng :ref:`class_skeletonprofilehumanoid`, auto-mapping sẽ được thực hiện khi
:ref:`class_skeletonprofile` is set. If the auto-mapping does not work well, you can map bones manually.

.. image:: img/retargeting2.webp

Mọi mapping quan hệ cha-con bị thiếu, trùng lặp hoặc không chính xác sẽ được chỉ báo bằng một button màu magenta / đỏ (tùy thuộc vào thiết lập của editor). Điều này không chặn quá trình import, nhưng cảnh báo rằng animation có thể không được chia sẻ chính xác.

.. note:: The auto-mapping uses pattern matching for the bone names. So we recommend
          sử dụng các tên tiếng Anh phổ biến cho bone.

Sau khi thiết lập ``bone_map``, một số tùy chọn sẽ có sẵn trong các section bên dưới.

.. image:: img/retargeting3.webp

Remove Tracks
~~~~~~~~~~~~~

Nếu bạn import resource dưới dạng :ref:`class_animationlibrary` sẽ được chia sẻ, chúng tôi khuyến nghị bật các tùy chọn này. Tuy nhiên, nếu bạn import resource dưới dạng scene, trong một số trường hợp nên tắt chúng. Ví dụ, nếu bạn import một character có accessory được animated, các tùy chọn này có thể khiến accessory không được animate.

Except Bone Transform
^^^^^^^^^^^^^^^^^^^^^

Xóa mọi track ngoại trừ track bone Transform khỏi các animation.

Unimportant Positions
^^^^^^^^^^^^^^^^^^^^^

Xóa các track Position khác với ``root_bone`` và ``scale_base_bone`` được định nghĩa trong :ref:`class_skeletonprofile` khỏi các animation. Trong :ref:`class_skeletonprofilehumanoid`, điều này có nghĩa là xóa các track Position khác với "Root" và "Hips". Kể từ Godot 4, animation bao gồm Bone Rest trong giá trị Transform. Nếu bạn tắt tùy chọn này, hình dạng cơ thể có thể thay đổi một cách khó đoán.

Unmapped Bones
^^^^^^^^^^^^^^

Xóa các track bone Transform chưa được mapping khỏi các animation.

Bone Renamer
~~~~~~~~~~~~

Rename Bones
^^^^^^^^^^^^

Đổi tên các bone đã được mapping.

Unique Node
^^^^^^^^^^^

Biến Skeleton thành một node duy nhất với tên được chỉ định trong ``skeleton_name``. Điều này cho phép thống nhất các path của animation track, không phụ thuộc vào hierarchy của scene.

Rest Fixer
~~~~~~~~~~

Các reference pose được định nghĩa trong :ref:`class_skeletonprofilehumanoid` tuân theo những quy tắc sau:

* Humanoid ở T-pose * Humanoid hướng về +Z trong Right-Handed Y-UP Coordinate System * Humanoid không được có Transform dưới dạng Node * Trục +Y hướng từ joint cha đến joint con * Rotation +X bẻ cong joint như một cơ đang co

Các quy tắc này là những định nghĩa thuận tiện cho blend animation và Inverse Kinematics (IK). Nếu model của bạn không khớp với định nghĩa này, bạn cần sửa nó bằng các tùy chọn này.

Apply Node Transform
^^^^^^^^^^^^^^^^^^^^

Nếu asset không được export đúng cách để chia sẻ, Skeleton được import có thể có một Transform dưới dạng Node. Ví dụ, glTF được export từ Blender mà không thực hiện "Apply Transform" là một trường hợp như vậy. Model có vẻ khớp với định nghĩa, nhưng các Transform nội bộ lại khác với định nghĩa. Tùy chọn này sửa các model như vậy bằng cách áp dụng Transform khi import.

.. note:: If the imported scene contains objects other than Skeletons, this option may have a negative effect.

Normalize Position Tracks
^^^^^^^^^^^^^^^^^^^^^^^^^

Track Position chủ yếu được dùng cho chuyển động của model, nhưng việc chia sẻ animation chuyển động giữa các model có chiều cao khác nhau có thể gây ra hiện tượng trượt do sự khác biệt về độ dài sải chân. Tùy chọn này chuẩn hóa các giá trị của track Position dựa trên chiều cao ``scale_base_bone``. Chiều cao ``scale_base_bone`` được lưu trong Skeleton dưới dạng ``motion_scale``, và các giá trị track Position đã chuẩn hóa được nhân với giá trị đó khi playback. Nếu tắt tùy chọn này, các track Position sẽ không được chuẩn hóa và ``motion_scale`` của Skeleton luôn được import dưới dạng ``1.0``.

Với :ref:`class_skeletonprofilehumanoid`, ``scale_base_bone`` là "Hips", do đó chiều cao của Hips được sử dụng làm ``motion_scale``.

Overwrite Axis
^^^^^^^^^^^^^^

Thống nhất Bone Rest của các model bằng cách ghi đè chúng để khớp với các reference pose được định nghĩa trong :ref:`class_skeletonprofile`.

.. note:: This is the most important option for sharing animations in Godot 4,
          nhưng hãy lưu ý rằng tùy chọn này có thể tạo ra kết quả tệ **nếu Bone Rest gốc được thiết lập bên ngoài là quan trọng**. Nếu bạn muốn chia sẻ animation mà vẫn giữ Bone Rest gốc, hãy cân nhắc sử dụng `Realtime Retarget Module <https://github.com/TokageItLab/realtime_retarget>`__.

Fix Silhouette
^^^^^^^^^^^^^^

Cố gắng làm cho silhouette của model khớp với silhouette của các reference pose được định nghĩa trong :ref:`class_skeletonprofile`, chẳng hạn như T-Pose. Tùy chọn này không thể sửa các silhouette quá khác biệt và có thể không hiệu quả trong việc sửa bone roll.

Với :ref:`class_skeletonprofilehumanoid`, tùy chọn này không cần được bật cho các model T-pose, nhưng nên được bật cho các model A-pose. Tuy nhiên, trong trường hợp đó, kết quả sửa foot có thể không tốt tùy thuộc vào chiều cao gót của model, vì vậy có thể cần thêm các tên bone :ref:`class_skeletonprofile` mà bạn không muốn sửa vào array ``filter``, như trong ví dụ bên dưới.

.. image:: img/retargeting4.webp

Ngoài ra, đối với các model có đầu gối hoặc bàn chân bị cong, có thể cần điều chỉnh chiều cao ``scale_base_bone``. Để làm vậy, bạn có thể sử dụng tùy chọn ``base_height_adjustment``.
