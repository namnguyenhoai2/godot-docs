:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CallbackTweener.xml.

.. _class_CallbackTweener:

CallbackTweener
===============

**Kế thừa:** :ref:`Tweener<class_Tweener>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Gọi method được chỉ định sau một khoảng trễ tùy chọn.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CallbackTweener** được dùng để gọi một method trong một chuỗi tween. Xem :ref:`Tween.tween_callback()<class_Tween_method_tween_callback>` để biết thêm thông tin về cách sử dụng.

Tweener sẽ tự động hoàn tất nếu object đích của callback được giải phóng.

\ **Lưu ý:** :ref:`Tween.tween_callback()<class_Tween_method_tween_callback>` là cách duy nhất đúng để tạo **CallbackTweener**. Bất kỳ **CallbackTweener** nào được tạo thủ công sẽ không hoạt động chính xác.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-----------------------------------------------+---------------------------------------------------------------------------------------------------+
   | :ref:`CallbackTweener<class_CallbackTweener>` | :ref:`set_delay<class_CallbackTweener_method_set_delay>`\ (\ delay\: :ref:`float<class_float>`\ ) |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_CallbackTweener_method_set_delay:

.. rst-class:: classref-method

:ref:`CallbackTweener<class_CallbackTweener>` **set_delay**\ (\ delay\: :ref:`float<class_float>`\ ) :ref:`🔗<class_CallbackTweener_method_set_delay>`

Tạo độ trễ cho lần gọi callback theo khoảng thời gian đã cho, tính bằng giây.

\ **Ví dụ:** Gọi :ref:`Node.queue_free()<class_Node_method_queue_free>` sau 2 giây:

::

    var tween = get_tree().create_tween()
    tween.tween_callback(queue_free).set_delay(2)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
