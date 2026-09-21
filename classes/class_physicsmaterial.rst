:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsMaterial.xml.

.. _class_PhysicsMaterial:

PhysicsMaterial
===============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lưu giữ các thuộc tính liên quan đến physics của một bề mặt, cụ thể là độ nhám và độ nảy của bề mặt đó.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu giữ các thuộc tính liên quan đến physics của một bề mặt, cụ thể là độ nhám và độ nảy của bề mặt đó. Class này được dùng để áp dụng các thuộc tính này cho một physics body.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`absorbent<class_PhysicsMaterial_property_absorbent>` | ``false`` |
   +---------------------------+------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`bounce<class_PhysicsMaterial_property_bounce>`       | ``0.0``   |
   +---------------------------+------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`friction<class_PhysicsMaterial_property_friction>`   | ``1.0``   |
   +---------------------------+------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`rough<class_PhysicsMaterial_property_rough>`         | ``false`` |
   +---------------------------+------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsMaterial_property_absorbent:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **absorbent** = ``false`` :ref:`🔗<class_PhysicsMaterial_property_absorbent>`

.. rst-class:: classref-property-setget

- |void| **set_absorbent**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_absorbent**\ (\ )

Nếu ``true``, trừ độ nảy của object va chạm khỏi độ nảy của object đó thay vì cộng thêm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsMaterial_property_bounce:

.. rst-class:: classref-property

:ref:`float<class_float>` **bounce** = ``0.0`` :ref:`🔗<class_PhysicsMaterial_property_bounce>`

.. rst-class:: classref-property-setget

- |void| **set_bounce**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bounce**\ (\ )

Độ nảy của body. Các giá trị nằm trong khoảng từ ``0`` (không nảy) đến ``1`` (độ nảy tối đa).

\ **Lưu ý:** Ngay cả khi :ref:`bounce<class_PhysicsMaterial_property_bounce>` được đặt thành ``1.0``, một phần năng lượng vẫn sẽ mất dần theo thời gian do linear damping và angular damping. Để có một physics body bảo toàn toàn bộ năng lượng theo thời gian, hãy đặt :ref:`bounce<class_PhysicsMaterial_property_bounce>` thành ``1.0``, linear damp mode của body thành **Replace** (nếu áp dụng), linear damp thành ``0.0``, angular damp mode thành **Replace** (nếu áp dụng), và angular damp thành ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsMaterial_property_friction:

.. rst-class:: classref-property

:ref:`float<class_float>` **friction** = ``1.0`` :ref:`🔗<class_PhysicsMaterial_property_friction>`

.. rst-class:: classref-property-setget

- |void| **set_friction**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_friction**\ (\ )

Độ ma sát của body. Các giá trị nằm trong khoảng từ ``0`` (không ma sát) đến ``1`` (ma sát tối đa).

.. rst-class:: classref-item-separator

----

.. _class_PhysicsMaterial_property_rough:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **rough** = ``false`` :ref:`🔗<class_PhysicsMaterial_property_rough>`

.. rst-class:: classref-property-setget

- |void| **set_rough**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_rough**\ (\ )

Nếu ``true``, physics engine sẽ sử dụng ma sát của object được đánh dấu là "rough" khi hai object va chạm. Nếu ``false``, physics engine sẽ sử dụng mức ma sát thấp nhất của tất cả các object đang va chạm. Nếu ``true`` cho cả hai object va chạm, physics engine sẽ sử dụng mức ma sát cao nhất.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
