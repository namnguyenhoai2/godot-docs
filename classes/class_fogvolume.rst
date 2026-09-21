:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FogVolume.xml.

.. _class_FogVolume:

FogVolume
=========

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một vùng đóng góp vào sương mù thể tích mặc định từ môi trường thế giới.

.. rst-class:: classref-introduction-group

Mô tả
-----

**FogVolume**\ s được dùng để thêm sương mù cục bộ vào hiệu ứng sương mù thể tích toàn cục. **FogVolume**\ s cũng có thể loại bỏ sương mù thể tích khỏi các khu vực cụ thể nếu sử dụng :ref:`FogMaterial<class_FogMaterial>` với :ref:`FogMaterial.density<class_FogMaterial_property_density>` âm.

Hiệu năng của **FogVolume**\ s liên quan trực tiếp đến kích thước tương đối của chúng trên màn hình và độ phức tạp của :ref:`FogMaterial<class_FogMaterial>` được gắn vào. Khi có thể, nên giữ **FogVolume**\ s tương đối nhỏ và đơn giản.

\ **Lưu ý:** **FogVolume**\ s chỉ có hiệu ứng hiển thị nếu :ref:`Environment.volumetric_fog_enabled<class_Environment_property_volumetric_fog_enabled>` là ``true``. Nếu không muốn sương mù hiển thị trên toàn cục (mà chỉ hiển thị bên trong các node **FogVolume**), hãy đặt :ref:`Environment.volumetric_fog_density<class_Environment_property_volumetric_fog_density>` thành ``0.0``.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sương mù thể tích và các volume sương mù <../tutorials/3d/volumetric_fog>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------+----------------------------------------------------+----------------------+
   | :ref:`Material<class_Material>`                            | :ref:`material<class_FogVolume_property_material>` |                      |
   +------------------------------------------------------------+----------------------------------------------------+----------------------+
   | :ref:`FogVolumeShape<enum_RenderingServer_FogVolumeShape>` | :ref:`shape<class_FogVolume_property_shape>`       | ``3``                |
   +------------------------------------------------------------+----------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                              | :ref:`size<class_FogVolume_property_size>`         | ``Vector3(2, 2, 2)`` |
   +------------------------------------------------------------+----------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FogVolume_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_FogVolume_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

:ref:`Material<class_Material>` được **FogVolume** sử dụng. Có thể là một :ref:`FogMaterial<class_FogMaterial>` dựng sẵn hoặc một :ref:`ShaderMaterial<class_ShaderMaterial>` tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_FogVolume_property_shape:

.. rst-class:: classref-property

:ref:`FogVolumeShape<enum_RenderingServer_FogVolumeShape>` **shape** = ``3`` :ref:`🔗<class_FogVolume_property_shape>`

.. rst-class:: classref-property-setget

- |void| **set_shape**\ (\ value\: :ref:`FogVolumeShape<enum_RenderingServer_FogVolumeShape>`\ ) - :ref:`FogVolumeShape<enum_RenderingServer_FogVolumeShape>` **get_shape**\ (\ )

Hình dạng của **FogVolume**. Có thể đặt thành :ref:`RenderingServer.FOG_VOLUME_SHAPE_ELLIPSOID<class_RenderingServer_constant_FOG_VOLUME_SHAPE_ELLIPSOID>`, :ref:`RenderingServer.FOG_VOLUME_SHAPE_CONE<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CONE>`, :ref:`RenderingServer.FOG_VOLUME_SHAPE_CYLINDER<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CYLINDER>`, :ref:`RenderingServer.FOG_VOLUME_SHAPE_BOX<class_RenderingServer_constant_FOG_VOLUME_SHAPE_BOX>` hoặc :ref:`RenderingServer.FOG_VOLUME_SHAPE_WORLD<class_RenderingServer_constant_FOG_VOLUME_SHAPE_WORLD>`.

.. rst-class:: classref-item-separator

----

.. _class_FogVolume_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_FogVolume_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của **FogVolume** khi :ref:`shape<class_FogVolume_property_shape>` là :ref:`RenderingServer.FOG_VOLUME_SHAPE_ELLIPSOID<class_RenderingServer_constant_FOG_VOLUME_SHAPE_ELLIPSOID>`, :ref:`RenderingServer.FOG_VOLUME_SHAPE_CONE<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CONE>`, :ref:`RenderingServer.FOG_VOLUME_SHAPE_CYLINDER<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CYLINDER>` hoặc :ref:`RenderingServer.FOG_VOLUME_SHAPE_BOX<class_RenderingServer_constant_FOG_VOLUME_SHAPE_BOX>`.

\ **Lưu ý:** Các volume sương mù mỏng có thể bị nhấp nháy khi camera di chuyển hoặc xoay. Có thể giảm hiện tượng này bằng cách tăng :ref:`ProjectSettings.rendering/environment/volumetric_fog/volume_depth<class_ProjectSettings_property_rendering/environment/volumetric_fog/volume_depth>` (đánh đổi bằng hiệu năng) hoặc giảm :ref:`Environment.volumetric_fog_length<class_Environment_property_volumetric_fog_length>` (không ảnh hưởng đến hiệu năng, nhưng làm giảm phạm vi sương mù). Ngoài ra, có thể làm **FogVolume** dày hơn và sử dụng density thấp hơn trong :ref:`material<class_FogVolume_property_material>`.

\ **Lưu ý:** Nếu :ref:`shape<class_FogVolume_property_shape>` là :ref:`RenderingServer.FOG_VOLUME_SHAPE_CONE<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CONE>` hoặc :ref:`RenderingServer.FOG_VOLUME_SHAPE_CYLINDER<class_RenderingServer_constant_FOG_VOLUME_SHAPE_CYLINDER>`, hình nón/hình trụ sẽ được điều chỉnh để nằm gọn trong kích thước. Không hỗ trợ scaling không đồng nhất của các hình dạng hình nón/hình trụ thông qua thuộc tính :ref:`size<class_FogVolume_property_size>`, nhưng bạn có thể scale node **FogVolume** thay thế.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
