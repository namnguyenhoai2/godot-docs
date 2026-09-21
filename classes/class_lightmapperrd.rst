:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/LightmapperRD.xml.

.. _class_LightmapperRD:

LightmapperRD
=============

**Kế thừa:** :ref:`Lightmapper<class_Lightmapper>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lightmapper dựa trên GPU tích hợp sẵn để sử dụng với :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

LightmapperRD ("RD" là viết tắt của :ref:`RenderingDevice<class_RenderingDevice>`) là lightmapper dựa trên GPU tích hợp sẵn để sử dụng với :ref:`LightmapGI<class_LightmapGI>`. Trên hầu hết các GPU chuyên dụng, nó có thể bake lightmap nhanh hơn nhiều so với hầu hết các lightmapper dựa trên CPU. LightmapperRD sử dụng compute shader để bake lightmap, vì vậy không yêu cầu cài đặt các thư viện CUDA hoặc OpenCL để có thể sử dụng.

\ **Lưu ý:** Lightmapper này yêu cầu GPU hỗ trợ backend :ref:`RenderingDevice<class_RenderingDevice>` (bộ render Forward+ và Mobile). Khi sử dụng Compatibility renderer, quá trình bake sẽ sử dụng một :ref:`RenderingDevice<class_RenderingDevice>` tạm thời. Không yêu cầu hỗ trợ :ref:`RenderingDevice<class_RenderingDevice>` để *render* các lightmap đã được bake trước đó.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
