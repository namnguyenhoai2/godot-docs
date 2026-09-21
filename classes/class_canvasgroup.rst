:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CanvasGroup.xml.

.. _class_CanvasGroup:

CanvasGroup
===========

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Gộp nhiều node 2D thành một thao tác vẽ duy nhất.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các node :ref:`CanvasItem<class_CanvasItem>` con của **CanvasGroup** được vẽ như một đối tượng duy nhất. Điều này cho phép, chẳng hạn, vẽ các node 2D trong mờ chồng lên nhau mà không khiến các vùng chồng lấp trở nên đục hơn dự kiến (đặt thuộc tính :ref:`CanvasItem.self_modulate<class_CanvasItem_property_self_modulate>` trên **CanvasGroup** để đạt được hiệu ứng này).

\ **Lưu ý:** **CanvasGroup** sử dụng một custom shader để đọc từ backbuffer nhằm vẽ các node con. Việc gán một :ref:`Material<class_Material>` cho **CanvasGroup** sẽ ghi đè shader tích hợp sẵn. Để sao chép hành vi của shader tích hợp sẵn trong một :ref:`Shader<class_Shader>` tùy chỉnh, hãy sử dụng đoạn sau:

::

    shader_type canvas_item;
    render_mode unshaded;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    void fragment() {
        vec4 c = textureLod(screen_texture, SCREEN_UV, 0.0);

        if (c.a > 0.0001) {
            c.rgb /= c.a;
        }

        COLOR *= c;
    }

\ **Lưu ý:** Vì **CanvasGroup** và :ref:`CanvasItem.clip_children<class_CanvasItem_property_clip_children>` đều sử dụng backbuffer, các node con của **CanvasGroup** có :ref:`CanvasItem.clip_children<class_CanvasItem_property_clip_children>` được đặt thành bất kỳ giá trị nào khác :ref:`CanvasItem.CLIP_CHILDREN_DISABLED<class_CanvasItem_constant_CLIP_CHILDREN_DISABLED>` sẽ không hoạt động chính xác.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`clear_margin<class_CanvasGroup_property_clear_margin>` | ``10.0``  |
   +---------------------------+--------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`fit_margin<class_CanvasGroup_property_fit_margin>`     | ``10.0``  |
   +---------------------------+--------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`use_mipmaps<class_CanvasGroup_property_use_mipmaps>`   | ``false`` |
   +---------------------------+--------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CanvasGroup_property_clear_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **clear_margin** = ``10.0`` :ref:`🔗<class_CanvasGroup_property_clear_margin>`

.. rst-class:: classref-property-setget

- |void| **set_clear_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_clear_margin**\ (\ )

Đặt kích thước của margin được dùng để mở rộng hình chữ nhật xóa của **CanvasGroup** này. Điều này mở rộng vùng backbuffer sẽ được **CanvasGroup** sử dụng. Margin nhỏ hơn sẽ giảm vùng backbuffer được sử dụng, từ đó có thể tăng hiệu năng; tuy nhiên, nếu :ref:`use_mipmaps<class_CanvasGroup_property_use_mipmaps>` được bật, margin nhỏ có thể gây ra lỗi mipmap ở cạnh của **CanvasGroup**. Vì vậy, nên để giá trị này nhỏ nhất có thể, nhưng cần tăng lên nếu xuất hiện lỗi hiển thị dọc theo các cạnh của canvas group.

.. rst-class:: classref-item-separator

----

.. _class_CanvasGroup_property_fit_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **fit_margin** = ``10.0`` :ref:`🔗<class_CanvasGroup_property_fit_margin>`

.. rst-class:: classref-property-setget

- |void| **set_fit_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fit_margin**\ (\ )

Đặt kích thước của margin được dùng để mở rộng hình chữ nhật có thể vẽ của **CanvasGroup** này. Kích thước của **CanvasGroup** được xác định bằng cách khớp một hình chữ nhật bao quanh các node con của nó, sau đó mở rộng hình chữ nhật đó thêm :ref:`fit_margin<class_CanvasGroup_property_fit_margin>`. Điều này làm tăng cả vùng backbuffer được sử dụng lẫn vùng được **CanvasGroup** bao phủ, và cả hai đều có thể làm giảm hiệu năng. Nên giữ giá trị này nhỏ nhất có thể và chỉ mở rộng khi cần kích thước lớn hơn (ví dụ: cho các hiệu ứng custom shader).

.. rst-class:: classref-item-separator

----

.. _class_CanvasGroup_property_use_mipmaps:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_mipmaps** = ``false`` :ref:`🔗<class_CanvasGroup_property_use_mipmaps>`

.. rst-class:: classref-property-setget

- |void| **set_use_mipmaps**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_mipmaps**\ (\ )

Nếu ``true``, tính toán mipmap cho backbuffer trước khi vẽ **CanvasGroup** để có thể sử dụng mipmap trong một :ref:`ShaderMaterial<class_ShaderMaterial>` tùy chỉnh được gắn vào **CanvasGroup**. Việc tạo mipmap có chi phí hiệu năng, vì vậy không nên bật tùy chọn này trừ khi cần thiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
