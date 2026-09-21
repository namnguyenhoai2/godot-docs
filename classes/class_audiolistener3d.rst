:github_url: hide

.. meta::
	:keywords: sound

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioListener3D.xml.

.. _class_AudioListener3D:

AudioListener3D
===============

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Ghi đè vị trí mà âm thanh được nghe từ đó.

.. rst-class:: classref-introduction-group

Mô tả
-----

Sau khi được thêm vào cây scene và bật bằng :ref:`make_current()<class_AudioListener3D_method_make_current>`, node này sẽ ghi đè vị trí mà âm thanh được nghe từ đó. Có thể dùng node này để lắng nghe từ một vị trí khác với :ref:`Camera3D<class_Camera3D>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------+--------------------------------------------------------------------------+-------+
   | :ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` | :ref:`doppler_tracking<class_AudioListener3D_property_doppler_tracking>` | ``0`` |
   +--------------------------------------------------------------+--------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+--------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`clear_current<class_AudioListener3D_method_clear_current>`\ (\ )                           |
   +---------------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>` | :ref:`get_listener_transform<class_AudioListener3D_method_get_listener_transform>`\ (\ ) |const| |
   +---------------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_current<class_AudioListener3D_method_is_current>`\ (\ ) |const|                         |
   +---------------------------------------+--------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`make_current<class_AudioListener3D_method_make_current>`\ (\ )                             |
   +---------------------------------------+--------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioListener3D_DopplerTracking:

.. rst-class:: classref-enumeration

enum **DopplerTracking**: :ref:`🔗<enum_AudioListener3D_DopplerTracking>`

.. _class_AudioListener3D_constant_DOPPLER_TRACKING_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` **DOPPLER_TRACKING_DISABLED** = ``0``

Tắt mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ (mặc định).

.. _class_AudioListener3D_constant_DOPPLER_TRACKING_IDLE_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` **DOPPLER_TRACKING_IDLE_STEP** = ``1``

Mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ bằng cách theo dõi vị trí của các đối tượng được thay đổi trong ``_process``. Những thay đổi về vận tốc tương đối của listener này so với các đối tượng đó sẽ ảnh hưởng đến cách cảm nhận âm thanh (thay đổi :ref:`AudioStreamPlayer3D.pitch_scale<class_AudioStreamPlayer3D_property_pitch_scale>` của âm thanh).

.. _class_AudioListener3D_constant_DOPPLER_TRACKING_PHYSICS_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` **DOPPLER_TRACKING_PHYSICS_STEP** = ``2``

Mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ bằng cách theo dõi vị trí của các đối tượng được thay đổi trong ``_physics_process``. Những thay đổi về vận tốc tương đối của listener này so với các đối tượng đó sẽ ảnh hưởng đến cách cảm nhận âm thanh (thay đổi :ref:`AudioStreamPlayer3D.pitch_scale<class_AudioStreamPlayer3D_property_pitch_scale>` của âm thanh).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioListener3D_property_doppler_tracking:

.. rst-class:: classref-property

:ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` **doppler_tracking** = ``0`` :ref:`🔗<class_AudioListener3D_property_doppler_tracking>`

.. rst-class:: classref-property-setget

- |void| **set_doppler_tracking**\ (\ value\: :ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>`\ ) - :ref:`DopplerTracking<enum_AudioListener3D_DopplerTracking>` **get_doppler_tracking**\ (\ )

Nếu không :ref:`DOPPLER_TRACKING_DISABLED<class_AudioListener3D_constant_DOPPLER_TRACKING_DISABLED>`, listener này sẽ mô phỏng `Doppler effect <https://en.wikipedia.org/wiki/Doppler_effect>`__ cho các đối tượng được thay đổi trong các phương thức ``_process`` cụ thể.

\ **Note:** The Doppler effect will only be heard on :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>`\ s if :ref:`AudioStreamPlayer3D.doppler_tracking<class_AudioStreamPlayer3D_property_doppler_tracking>` is not set to :ref:`AudioStreamPlayer3D.DOPPLER_TRACKING_DISABLED<class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_DISABLED>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioListener3D_method_clear_current:

.. rst-class:: classref-method

|void| **clear_current**\ (\ ) :ref:`🔗<class_AudioListener3D_method_clear_current>`

Tắt listener để thay vào đó sử dụng listener của camera hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_AudioListener3D_method_get_listener_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **get_listener_transform**\ (\ ) |const| :ref:`🔗<class_AudioListener3D_method_get_listener_transform>`

Trả về :ref:`Transform3D<class_Transform3D>` trực chuẩn hóa toàn cục của listener.

.. rst-class:: classref-item-separator

----

.. _class_AudioListener3D_method_is_current:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_current**\ (\ ) |const| :ref:`🔗<class_AudioListener3D_method_is_current>`

Trả về ``true`` nếu listener được đặt thành hiện tại bằng :ref:`make_current()<class_AudioListener3D_method_make_current>`, nếu không thì trả về ``false``.

\ **Lưu ý:** Có thể có nhiều AudioListener3D được đánh dấu là "current" trong cây scene, nhưng chỉ listener được đặt thành hiện tại sau cùng mới được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_AudioListener3D_method_make_current:

.. rst-class:: classref-method

|void| **make_current**\ (\ ) :ref:`🔗<class_AudioListener3D_method_make_current>`

Bật listener. Thao tác này sẽ ghi đè listener của camera hiện tại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
