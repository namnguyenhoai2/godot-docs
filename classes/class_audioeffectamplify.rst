:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectAmplify.xml.

.. _class_AudioEffectAmplify:

AudioEffectAmplify
==================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng xử lý âm lượng vào một audio bus.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tăng hoặc giảm âm lượng được định tuyến qua audio bus.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`volume_db<class_AudioEffectAmplify_property_volume_db>`         | ``0.0`` |
   +---------------------------+-----------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`volume_linear<class_AudioEffectAmplify_property_volume_linear>` |         |
   +---------------------------+-----------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectAmplify_property_volume_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_db** = ``0.0`` :ref:`🔗<class_AudioEffectAmplify_property_volume_db>`

.. rst-class:: classref-property-setget

- |void| **set_volume_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_db**\ (\ )

Mức khuếch đại tính bằng dB. Giá trị dương làm âm thanh to hơn, giá trị âm làm âm thanh nhỏ hơn. Giá trị có thể nằm trong khoảng từ -80 đến 24.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectAmplify_property_volume_linear:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_linear** :ref:`🔗<class_AudioEffectAmplify_property_volume_linear>`

.. rst-class:: classref-property-setget

- |void| **set_volume_linear**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_linear**\ (\ )

Mức khuếch đại dưới dạng giá trị tuyến tính.

\ **Lưu ý:** Thành viên này sửa đổi :ref:`volume_db<class_AudioEffectAmplify_property_volume_db>` để thuận tiện. Giá trị được trả về tương đương với kết quả của :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` trên :ref:`volume_db<class_AudioEffectAmplify_property_volume_db>`. Việc thiết lập thành viên này tương đương với việc thiết lập :ref:`volume_db<class_AudioEffectAmplify_property_volume_db>` thành kết quả của :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>` trên một giá trị.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
