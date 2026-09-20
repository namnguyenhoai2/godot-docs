.. _doc_exporting_3d_scenes:

Xuất scene 3D
=============

Tổng quan
---------

Trong Godot, bạn có thể xuất scene 3D dưới dạng tệp glTF 2.0. Bạn có thể xuất dưới dạng glTF binary (``.glb`` file) hoặc glTF nhúng texture (``gltf`` + ``.bin`` + textures). Điều này cho phép bạn tạo scene trong Godot, chẳng hạn như blockout khối lưới CSG cho một level, xuất scene đó để chỉnh sửa trong một chương trình như Blender, rồi đưa trở lại Godot.

.. note::

    Chỉ Blender 2.83 trở lên mới có thể import các tệp glTF được Godot xuất.

Để xuất một scene trong editor, hãy vào **Scene > Export As... > glTF 2.0 Scene...**

.. image:: img/gltf_godot_export.png

Hạn chế
-------

glTF export có một số hạn chế.

* Không hỗ trợ xuất particles vì cách triển khai của chúng khác nhau giữa các engine. * Không thể xuất ShaderMaterials. * Không hỗ trợ xuất scene 2D.

.. seealso::

    Các scene 3D có thể được lưu trong runtime bằng cách sử dụng
    :ref:`runtime file loading and saving <doc_runtime_file_loading_and_saving_3d_scenes>`,
    bao gồm cả từ một project đã được export.
