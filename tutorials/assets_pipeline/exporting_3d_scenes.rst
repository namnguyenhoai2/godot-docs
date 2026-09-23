.. _doc_exporting_3d_scenes:

Xuất cảnh 3D
============

Tổng quan
---------

Trong Godot, bạn có thể xuất các cảnh 3D dưới dạng tệp glTF 2.0. Bạn có thể xuất dưới dạng glTF binary (``.glb`` tệp) hoặc glTF nhúng texture (``gltf`` + ``.bin`` + texture). Điều này cho phép bạn tạo các cảnh trong Godot, chẳng hạn như bản dựng thô một màn chơi bằng khối lưới CSG, xuất cảnh đó để hoàn thiện trong một chương trình như Blender, rồi đưa cảnh trở lại Godot.

.. note::

    Chỉ Blender 2.83 trở lên mới có thể nhập các tệp glTF được Godot xuất.

Để xuất một cảnh trong editor, hãy vào **Scene > Export As... > glTF 2.0 Scene...**

.. image:: img/gltf_godot_export.png

Giới hạn
--------

Tính năng xuất glTF có một số giới hạn.

* Không hỗ trợ xuất particle vì cách triển khai của chúng khác nhau giữa các engine.
* Không thể xuất ShaderMaterials.
* Không hỗ trợ xuất các cảnh 2D.

.. seealso::

    Các cảnh 3D có thể được lưu trong runtime bằng
    :ref:`tải và lưu tệp trong runtime <doc_runtime_file_loading_and_saving_3d_scenes>`, kể cả từ một project đã xuất.
