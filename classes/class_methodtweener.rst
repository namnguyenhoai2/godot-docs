:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/MethodTweener.xml.

.. _class_MethodTweener:

MethodTweener
=============

**Kế thừa:** :ref:`Tweener<class_Tweener>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Nội suy một giá trị trừu tượng và cung cấp giá trị đó cho một phương thức được gọi theo thời gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

**MethodTweener** tương tự như sự kết hợp giữa :ref:`CallbackTweener<class_CallbackTweener>` và :ref:`PropertyTweener<class_PropertyTweener>`. Nó gọi một phương thức và cung cấp một giá trị đã nội suy làm tham số. Xem :ref:`Tween.tween_method()<class_Tween_method_tween_method>` để biết thêm thông tin về cách sử dụng.

Tweener sẽ tự động kết thúc nếu đối tượng đích của callback được giải phóng.

\ **Lưu ý:** :ref:`Tween.tween_method()<class_Tween_method_tween_method>` là cách duy nhất đúng để tạo **MethodTweener**. Mọi **MethodTweener** được tạo thủ công sẽ không hoạt động chính xác.

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MethodTweener<class_MethodTweener>` | :ref:`set_delay<class_MethodTweener_method_set_delay>`\ (\ delay\: :ref:`float<class_float>`\ )                        |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MethodTweener<class_MethodTweener>` | :ref:`set_ease<class_MethodTweener_method_set_ease>`\ (\ ease\: :ref:`EaseType<enum_Tween_EaseType>`\ )                |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MethodTweener<class_MethodTweener>` | :ref:`set_trans<class_MethodTweener_method_set_trans>`\ (\ trans\: :ref:`TransitionType<enum_Tween_TransitionType>`\ ) |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MethodTweener_method_set_delay:

.. rst-class:: classref-method

:ref:`MethodTweener<class_MethodTweener>` **set_delay**\ (\ delay\: :ref:`float<class_float>`\ ) :ref:`🔗<class_MethodTweener_method_set_delay>`

Đặt khoảng thời gian tính bằng giây trước khi **MethodTweener** bắt đầu nội suy. Theo mặc định, không có độ trễ.

.. rst-class:: classref-item-separator

----

.. _class_MethodTweener_method_set_ease:

.. rst-class:: classref-method

:ref:`MethodTweener<class_MethodTweener>` **set_ease**\ (\ ease\: :ref:`EaseType<enum_Tween_EaseType>`\ ) :ref:`🔗<class_MethodTweener_method_set_ease>`

Đặt kiểu easing được sử dụng từ :ref:`EaseType<enum_Tween_EaseType>`. Nếu không được đặt, easing mặc định từ :ref:`Tween<class_Tween>` chứa Tweener này sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_MethodTweener_method_set_trans:

.. rst-class:: classref-method

:ref:`MethodTweener<class_MethodTweener>` **set_trans**\ (\ trans\: :ref:`TransitionType<enum_Tween_TransitionType>`\ ) :ref:`🔗<class_MethodTweener_method_set_trans>`

Đặt kiểu transition được sử dụng từ :ref:`TransitionType<enum_Tween_TransitionType>`. Nếu không được đặt, transition mặc định từ :ref:`Tween<class_Tween>` chứa Tweener này sẽ được sử dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
