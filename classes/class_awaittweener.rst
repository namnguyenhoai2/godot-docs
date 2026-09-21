:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AwaitTweener.xml.

.. _class_AwaitTweener:

AwaitTweener
============

**Kế thừa:** :ref:`Tweener<class_Tweener>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Chờ một tín hiệu được chỉ định.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AwaitTweener** được sử dụng để chờ một tín hiệu được chỉ định, cho phép thực hiện các bước bất đồng bộ trong animation của :ref:`Tween<class_Tween>`. Xem :ref:`Tween.tween_await()<class_Tween_method_tween_await>` để biết thêm thông tin về cách sử dụng.

Tín hiệu :ref:`Tweener.finished<class_Tweener_signal_finished>` được phát ra khi nhận được tín hiệu đang chờ, khi đạt đến thời gian chờ hoặc khi đối tượng đích được giải phóng.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------+------------------------------------------------------------------------------------------------------+
   | :ref:`AwaitTweener<class_AwaitTweener>` | :ref:`set_timeout<class_AwaitTweener_method_set_timeout>`\ (\ timeout\: :ref:`float<class_float>`\ ) |
   +-----------------------------------------+------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_AwaitTweener_method_set_timeout:

.. rst-class:: classref-method

:ref:`AwaitTweener<class_AwaitTweener>` **set_timeout**\ (\ timeout\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AwaitTweener_method_set_timeout>`

Đặt khoảng thời gian tối đa mà một **AwaitTweener** có thể chờ tín hiệu. Có thể sử dụng để bảo vệ trong trường hợp các tín hiệu có thể không bao giờ được phát ra. Nếu không được chỉ định, tweener sẽ chờ vô thời hạn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
