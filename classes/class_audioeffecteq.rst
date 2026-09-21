:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectEQ.xml.

.. _class_AudioEffectEQ:

AudioEffectEQ
=============

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioEffectEQ10<class_AudioEffectEQ10>`, :ref:`AudioEffectEQ21<class_AudioEffectEQ21>`, :ref:`AudioEffectEQ6<class_AudioEffectEQ6>`

Lớp cơ sở cho các bộ cân bằng âm thanh (EQ). Cho phép bạn kiểm soát các tần số.

Sử dụng lớp này để tạo một bộ cân bằng tùy chỉnh nếu :ref:`AudioEffectEQ6<class_AudioEffectEQ6>`, :ref:`AudioEffectEQ10<class_AudioEffectEQ10>` hoặc :ref:`AudioEffectEQ21<class_AudioEffectEQ21>` không đáp ứng nhu cầu của bạn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một "bộ cân bằng" cho phép bạn kiểm soát gain của các tần số trong toàn bộ phổ tần bằng cách điều chỉnh chúng thông qua các dải tần. Một dải tần là một điểm trong phổ tần, và mỗi dải tần biểu thị một phần của phổ có thể được điều chỉnh.

Sử dụng các bộ cân bằng để bù đắp những thiếu sót hiện có trong âm thanh, tạo khoảng trống cho các thành phần khác hoặc loại bỏ những tần số không mong muốn. AudioEffectEQ hữu ích trên bus Master để cân bằng toàn bộ bản mix hoặc tạo thêm cá tính cho mix. Chúng cũng hữu ích khi chạy game trên thiết bị di động, nhằm điều chỉnh mix cho phù hợp với loại loa đó (có thể tắt khi cắm tai nghe).

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_band_count<class_AudioEffectEQ_method_get_band_count>`\ (\ ) |const|                                                                      |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_band_gain_db<class_AudioEffectEQ_method_get_band_gain_db>`\ (\ band_idx\: :ref:`int<class_int>`\ ) |const|                                |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_band_gain_db<class_AudioEffectEQ_method_set_band_gain_db>`\ (\ band_idx\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ ) |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffectEQ_method_get_band_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_band_count**\ (\ ) |const| :ref:`🔗<class_AudioEffectEQ_method_get_band_count>`

Trả về số lượng dải tần của bộ cân bằng.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectEQ_method_get_band_gain_db:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_band_gain_db**\ (\ band_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioEffectEQ_method_get_band_gain_db>`

Trả về gain của dải tần tại chỉ mục được chỉ định, tính bằng dB.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectEQ_method_set_band_gain_db:

.. rst-class:: classref-method

|void| **set_band_gain_db**\ (\ band_idx\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioEffectEQ_method_set_band_gain_db>`

Thiết lập gain của dải tần tại chỉ mục được chỉ định, tính bằng dB.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
