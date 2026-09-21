:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Material.xml.

.. _class_Material:

Material
========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`BaseMaterial3D<class_BaseMaterial3D>`, :ref:`BlitMaterial<class_BlitMaterial>`, :ref:`CanvasItemMaterial<class_CanvasItemMaterial>`, :ref:`FogMaterial<class_FogMaterial>`, :ref:`PanoramaSkyMaterial<class_PanoramaSkyMaterial>`, :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>`, :ref:`PhysicalSkyMaterial<class_PhysicalSkyMaterial>`, :ref:`PlaceholderMaterial<class_PlaceholderMaterial>`, :ref:`ProceduralSkyMaterial<class_ProceduralSkyMaterial>`, :ref:`ShaderMaterial<class_ShaderMaterial>`

Lớp cơ sở ảo để áp dụng các thuộc tính hiển thị cho một đối tượng, chẳng hạn như màu sắc và độ nhám.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Material** là một resource cơ sở được dùng để tô màu và tạo bóng cho hình học. Tất cả material đều kế thừa từ nó và hầu hết các node dẫn xuất từ :ref:`VisualInstance3D<class_VisualInstance3D>` đều mang một **Material**. Một vài cờ và tham số được dùng chung giữa tất cả các loại material và được cấu hình tại đây.

Điều quan trọng là bạn có thể kế thừa từ **Material** để tạo kiểu material tùy chỉnh của riêng mình bằng script hoặc trong GDExtension.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D Material Testers Demo <https://godotengine.org/asset-library/asset/2742>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+-----------------------------------------------------------------+
   | :ref:`Material<class_Material>` | :ref:`next_pass<class_Material_property_next_pass>`             |
   +---------------------------------+-----------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`render_priority<class_Material_property_render_priority>` |
   +---------------------------------+-----------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`_can_do_next_pass<class_Material_private_method__can_do_next_pass>`\ (\ ) |virtual| |const|               |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`_can_use_render_priority<class_Material_private_method__can_use_render_priority>`\ (\ ) |virtual| |const| |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Mode<enum_Shader_Mode>`   | :ref:`_get_shader_mode<class_Material_private_method__get_shader_mode>`\ (\ ) |virtual| |required| |const|      |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`           | :ref:`_get_shader_rid<class_Material_private_method__get_shader_rid>`\ (\ ) |virtual| |required| |const|        |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>` | :ref:`create_placeholder<class_Material_method_create_placeholder>`\ (\ ) |const|                               |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`inspect_native_shader_code<class_Material_method_inspect_native_shader_code>`\ (\ )                       |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_Material_constant_RENDER_PRIORITY_MAX:

.. rst-class:: classref-constant

**RENDER_PRIORITY_MAX** = ``127`` :ref:`🔗<class_Material_constant_RENDER_PRIORITY_MAX>`

Giá trị lớn nhất cho tham số :ref:`render_priority<class_Material_property_render_priority>`.

.. _class_Material_constant_RENDER_PRIORITY_MIN:

.. rst-class:: classref-constant

**RENDER_PRIORITY_MIN** = ``-128`` :ref:`🔗<class_Material_constant_RENDER_PRIORITY_MIN>`

Giá trị nhỏ nhất cho tham số :ref:`render_priority<class_Material_property_render_priority>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Material_property_next_pass:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **next_pass** :ref:`🔗<class_Material_property_next_pass>`

.. rst-class:: classref-property-setget

- |void| **set_next_pass**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_next_pass**\ (\ )

Đặt **Material** sẽ được sử dụng cho pass tiếp theo. Thao tác này render đối tượng một lần nữa bằng một material khác.

\ **Lưu ý:** Các material :ref:`next_pass<class_Material_property_next_pass>` không nhất thiết được vẽ ngay sau **Material** nguồn. Thứ tự vẽ được xác định bởi các thuộc tính material, :ref:`render_priority<class_Material_property_render_priority>`, và khoảng cách đến camera.

\ **Lưu ý:** Điều này chỉ áp dụng cho :ref:`StandardMaterial3D<class_StandardMaterial3D>`\ s và :ref:`ShaderMaterial<class_ShaderMaterial>`\ s có kiểu "Spatial".

.. rst-class:: classref-item-separator

----

.. _class_Material_property_render_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **render_priority** :ref:`🔗<class_Material_property_render_priority>`

.. rst-class:: classref-property-setget

- |void| **set_render_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_render_priority**\ (\ )

Đặt mức độ ưu tiên render cho các đối tượng trong scene 3D. Các đối tượng có mức ưu tiên cao hơn sẽ được sắp xếp phía trước các đối tượng có mức ưu tiên thấp hơn. Nói cách khác, tất cả các đối tượng có :ref:`render_priority<class_Material_property_render_priority>` ``1`` sẽ được render bên trên tất cả các đối tượng có :ref:`render_priority<class_Material_property_render_priority>` ``0``.

\ **Lưu ý:** Điều này chỉ áp dụng cho :ref:`StandardMaterial3D<class_StandardMaterial3D>`\ s và :ref:`ShaderMaterial<class_ShaderMaterial>`\ s có kiểu "Spatial".

\ **Lưu ý:** Điều này không ảnh hưởng đến cách các đối tượng trong suốt được sắp xếp tương đối với các đối tượng đục, hoặc cách các mesh động được sắp xếp tương đối với các mesh đục khác. Nguyên nhân là tất cả đối tượng trong suốt đều được vẽ sau tất cả đối tượng đục, còn tất cả mesh đục động đều được vẽ trước các mesh đục khác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Material_private_method__can_do_next_pass:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_do_next_pass**\ (\ ) |virtual| |const| :ref:`🔗<class_Material_private_method__can_do_next_pass>`

Chỉ được expose nhằm mục đích override. Bạn không thể gọi trực tiếp hàm này. Được sử dụng nội bộ để xác định xem :ref:`next_pass<class_Material_property_next_pass>` có nên được hiển thị trong editor hay không.

.. rst-class:: classref-item-separator

----

.. _class_Material_private_method__can_use_render_priority:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_use_render_priority**\ (\ ) |virtual| |const| :ref:`🔗<class_Material_private_method__can_use_render_priority>`

Chỉ được expose nhằm mục đích override. Bạn không thể gọi trực tiếp hàm này. Được sử dụng nội bộ để xác định xem :ref:`render_priority<class_Material_property_render_priority>` có nên được hiển thị trong editor hay không.

.. rst-class:: classref-item-separator

----

.. _class_Material_private_method__get_shader_mode:

.. rst-class:: classref-method

:ref:`Mode<enum_Shader_Mode>` **_get_shader_mode**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_Material_private_method__get_shader_mode>`

Chỉ được expose nhằm mục đích override. Bạn không thể gọi trực tiếp hàm này. Được các công cụ editor khác nhau sử dụng nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_Material_private_method__get_shader_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **_get_shader_rid**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_Material_private_method__get_shader_rid>`

Chỉ được expose nhằm mục đích override. Bạn không thể gọi trực tiếp hàm này. Được các công cụ editor khác nhau sử dụng nội bộ. Dùng để truy cập RID của :ref:`Shader<class_Shader>` của **Material**.

.. rst-class:: classref-item-separator

----

.. _class_Material_method_create_placeholder:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **create_placeholder**\ (\ ) |const| :ref:`🔗<class_Material_method_create_placeholder>`

Tạo một phiên bản placeholder của resource này (:ref:`PlaceholderMaterial<class_PlaceholderMaterial>`).

.. rst-class:: classref-item-separator

----

.. _class_Material_method_inspect_native_shader_code:

.. rst-class:: classref-method

|void| **inspect_native_shader_code**\ (\ ) :ref:`🔗<class_Material_method_inspect_native_shader_code>`

Chỉ khả dụng khi chạy trong editor. Mở một popup trực quan hóa mã shader được tạo, bao gồm tất cả các variant và mã shader nội bộ. Xem thêm :ref:`Shader.inspect_native_shader_code()<class_Shader_method_inspect_native_shader_code>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
