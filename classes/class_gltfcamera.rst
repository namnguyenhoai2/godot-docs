:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gltf/doc_classes/GLTFCamera.xml.

.. _class_GLTFCamera:

GLTFCamera
==========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một camera glTF.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho một camera như được định nghĩa trong đặc tả glTF cơ sở.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Tải và lưu tệp runtime <../tutorials/io/runtime_file_loading_and_saving>`

- `glTF camera detailed specification <https://registry.khronos.org/glTF/specs/2.0/glTF-2.0.html#reference-camera>`__

- `glTF camera spec and example file <https://github.com/KhronosGroup/glTF-Tutorials/blob/master/gltfTutorial/gltfTutorial_015_SimpleCameras.md>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`depth_far<class_GLTFCamera_property_depth_far>`     | ``4000.0``    |
   +---------------------------+-----------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`depth_near<class_GLTFCamera_property_depth_near>`   | ``0.05``      |
   +---------------------------+-----------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`fov<class_GLTFCamera_property_fov>`                 | ``1.3089969`` |
   +---------------------------+-----------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`   | :ref:`perspective<class_GLTFCamera_property_perspective>` | ``true``      |
   +---------------------------+-----------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`size_mag<class_GLTFCamera_property_size_mag>`       | ``0.5``       |
   +---------------------------+-----------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFCamera<class_GLTFCamera>` | :ref:`from_dictionary<class_GLTFCamera_method_from_dictionary>`\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`GLTFCamera<class_GLTFCamera>` | :ref:`from_node<class_GLTFCamera_method_from_node>`\ (\ camera_node\: :ref:`Camera3D<class_Camera3D>`\ ) |static|                |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`to_dictionary<class_GLTFCamera_method_to_dictionary>`\ (\ ) |const|                                                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Camera3D<class_Camera3D>`     | :ref:`to_node<class_GLTFCamera_method_to_node>`\ (\ ) |const|                                                                    |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GLTFCamera_property_depth_far:

.. rst-class:: classref-property

:ref:`float<class_float>` **depth_far** = ``4000.0`` :ref:`🔗<class_GLTFCamera_property_depth_far>`

.. rst-class:: classref-property-setget

- |void| **set_depth_far**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_depth_far**\ (\ )

Khoảng cách đến ranh giới culling xa đối với camera này theo trục Z cục bộ của nó, tính bằng mét. Giá trị này ánh xạ tới thuộc tính ``zfar`` của glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_property_depth_near:

.. rst-class:: classref-property

:ref:`float<class_float>` **depth_near** = ``0.05`` :ref:`🔗<class_GLTFCamera_property_depth_near>`

.. rst-class:: classref-property-setget

- |void| **set_depth_near**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_depth_near**\ (\ )

Khoảng cách đến ranh giới culling gần đối với camera này theo trục Z cục bộ của nó, tính bằng mét. Giá trị này ánh xạ tới thuộc tính ``znear`` của glTF.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_property_fov:

.. rst-class:: classref-property

:ref:`float<class_float>` **fov** = ``1.3089969`` :ref:`🔗<class_GLTFCamera_property_fov>`

.. rst-class:: classref-property-setget

- |void| **set_fov**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fov**\ (\ )

FOV của camera. Class này và glTF định nghĩa FOV của camera theo radian, trong khi Godot sử dụng độ. Giá trị này ánh xạ tới thuộc tính ``yfov`` của glTF. Giá trị này chỉ được sử dụng cho camera phối cảnh, khi :ref:`perspective<class_GLTFCamera_property_perspective>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_property_perspective:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **perspective** = ``true`` :ref:`🔗<class_GLTFCamera_property_perspective>`

.. rst-class:: classref-property-setget

- |void| **set_perspective**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_perspective**\ (\ )

Nếu ``true``, camera ở chế độ phối cảnh. Nếu không, camera ở chế độ trực giao/orthogonal. Giá trị này ánh xạ tới thuộc tính ``type`` của camera glTF. Xem :ref:`Camera3D.projection<class_Camera3D_property_projection>` và đặc tả glTF để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_property_size_mag:

.. rst-class:: classref-property

:ref:`float<class_float>` **size_mag** = ``0.5`` :ref:`🔗<class_GLTFCamera_property_size_mag>`

.. rst-class:: classref-property-setget

- |void| **set_size_mag**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_size_mag**\ (\ )

Kích thước của camera. Class này và glTF định nghĩa độ lớn kích thước camera là bán kính tính bằng mét, trong khi Godot định nghĩa đó là đường kính tính bằng mét. Giá trị này ánh xạ tới thuộc tính ``ymag`` của glTF. Giá trị này chỉ được sử dụng cho camera trực giao/orthogonal, khi :ref:`perspective<class_GLTFCamera_property_perspective>` là ``false``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GLTFCamera_method_from_dictionary:

.. rst-class:: classref-method

:ref:`GLTFCamera<class_GLTFCamera>` **from_dictionary**\ (\ dictionary\: :ref:`Dictionary<class_Dictionary>`\ ) |static| :ref:`🔗<class_GLTFCamera_method_from_dictionary>`

Tạo một instance GLTFCamera mới bằng cách phân tích :ref:`Dictionary<class_Dictionary>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_method_from_node:

.. rst-class:: classref-method

:ref:`GLTFCamera<class_GLTFCamera>` **from_node**\ (\ camera_node\: :ref:`Camera3D<class_Camera3D>`\ ) |static| :ref:`🔗<class_GLTFCamera_method_from_node>`

Tạo một instance GLTFCamera mới từ node :ref:`Camera3D<class_Camera3D>` Godot đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_method_to_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **to_dictionary**\ (\ ) |const| :ref:`🔗<class_GLTFCamera_method_to_dictionary>`

Tuần tự hóa instance GLTFCamera này thành một :ref:`Dictionary<class_Dictionary>`.

.. rst-class:: classref-item-separator

----

.. _class_GLTFCamera_method_to_node:

.. rst-class:: classref-method

:ref:`Camera3D<class_Camera3D>` **to_node**\ (\ ) |const| :ref:`🔗<class_GLTFCamera_method_to_node>`

Chuyển đổi instance GLTFCamera này thành một node :ref:`Camera3D<class_Camera3D>` Godot.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
