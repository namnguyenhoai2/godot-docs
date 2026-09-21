:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Lightmapper.xml.

.. _class_Lightmapper:

Lightmapper
===========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`LightmapperRD<class_LightmapperRD>`

Lớp trừu tượng được các lightmapper mở rộng để sử dụng trong :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này nên được mở rộng bởi các lớp lightmapper tùy chỉnh. Sau đó, có thể sử dụng lightmapper với :ref:`LightmapGI<class_LightmapGI>` để cung cấp global illumination được bake nhanh trong 3D.

Godot có một lightmapper dựa trên GPU tích hợp sẵn là :ref:`LightmapperRD<class_LightmapperRD>`, sử dụng compute shader, nhưng có thể triển khai các lightmapper tùy chỉnh bằng các module C++.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
