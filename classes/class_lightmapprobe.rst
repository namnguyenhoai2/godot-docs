:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LightmapProbe.xml.

.. _class_LightmapProbe:

LightmapProbe
=============

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đại diện cho một probe được đặt thủ công để chiếu sáng đối tượng động với :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**LightmapProbe** đại diện cho vị trí của một probe được đặt thủ công để chiếu sáng đối tượng động với :ref:`LightmapGI<class_LightmapGI>`. Các lightmap probe ảnh hưởng đến việc chiếu sáng của các node bắt nguồn từ :ref:`GeometryInstance3D<class_GeometryInstance3D>` có :ref:`GeometryInstance3D.gi_mode<class_GeometryInstance3D_property_gi_mode>` được đặt thành :ref:`GeometryInstance3D.GI_MODE_DYNAMIC<class_GeometryInstance3D_constant_GI_MODE_DYNAMIC>`.

Thông thường, các probe :ref:`LightmapGI<class_LightmapGI>` được tự động đặt bằng cách đặt :ref:`LightmapGI.generate_probes_subdiv<class_LightmapGI_property_generate_probes_subdiv>` thành một giá trị khác :ref:`LightmapGI.GENERATE_PROBES_DISABLED<class_LightmapGI_constant_GENERATE_PROBES_DISABLED>`. Bằng cách tạo các node **LightmapProbe** trước khi bake lightmap, bạn có thể thêm nhiều probe hơn vào các khu vực cụ thể để có độ chi tiết cao hơn, hoặc tắt tính năng tự động tạo và chỉ sử dụng các probe được đặt thủ công.

\ **Lưu ý:** Các node **LightmapProbe**\ s được đặt sau khi bake lightmap sẽ bị các đối tượng động bỏ qua. Bạn phải bake lightmap lại sau khi tạo hoặc sửa đổi các **LightmapProbe**\ s để các probe có hiệu lực.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
