:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/bool.xml.

.. _class_bool:

bool
====

Một kiểu boolean được tích hợp sẵn.

.. rst-class:: classref-introduction-group

Mô tả
-----

**bool** là một kiểu :ref:`Variant<class_Variant>` được tích hợp sẵn, chỉ có thể lưu trữ một trong hai giá trị: ``true`` hoặc ``false``. Bạn có thể hình dung nó như một công tắc chỉ có thể bật hoặc tắt, hoặc như một chữ số nhị phân chỉ có thể là 1 hoặc 0.

Có thể sử dụng trực tiếp các giá trị boolean trong ``if`` và các câu lệnh điều kiện khác:


.. tabs::

 .. code-tab:: gdscript

    var can_shoot = true
    if can_shoot:
        launch_bullet()

 .. code-tab:: csharp

    bool canShoot = true;
    if (canShoot)
    {
        LaunchBullet();
    }



Tất cả các toán tử so sánh đều trả về giá trị boolean (``==``, ``>``, ``<=``, v.v.). Vì vậy, không cần phải so sánh chính các giá trị boolean. Bạn không cần thêm ``== true`` hoặc ``== false``.

Có thể kết hợp các giá trị boolean bằng các toán tử logic ``and``, ``or``, ``not`` để tạo ra các điều kiện phức tạp:


.. tabs::

 .. code-tab:: gdscript

    if bullets > 0 and not is_reloading():
        launch_bullet()

    if bullets == 0 or is_reloading():
        play_clack_sound()

 .. code-tab:: csharp

    if (bullets > 0 && !IsReloading())
    {
        LaunchBullet();
    }

    if (bullets == 0 || IsReloading())
    {
        PlayClackSound();
    }



\ **Lưu ý:** Trong các ngôn ngữ lập trình hiện đại, các toán tử logic được đánh giá theo thứ tự. Tất cả các điều kiện còn lại sẽ được bỏ qua nếu kết quả của chúng không thể ảnh hưởng đến giá trị cuối cùng. Khái niệm này được gọi là `short-circuit evaluation <https://en.wikipedia.org/wiki/Short-circuit_evaluation>`__ và có thể hữu ích để tránh đánh giá các điều kiện tốn kém trong một số trường hợp cần tối ưu hiệu năng.

\ **Lưu ý:** Theo quy ước, các method và property tích hợp sẵn trả về giá trị boolean thường được định nghĩa dưới dạng câu hỏi có- không, tính từ đơn hoặc dạng tương tự (:ref:`String.is_empty()<class_String_method_is_empty>`, :ref:`Node.can_process()<class_Node_method_can_process>`, :ref:`Camera2D.enabled<class_Camera2D_property_enabled>`, v.v.).

.. rst-class:: classref-reftable-group

Constructors
------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`bool<class_bool_constructor_bool>`\ (\ )                                   |
   +-------------------------+----------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`bool<class_bool_constructor_bool>`\ (\ from\: :ref:`bool<class_bool>`\ )   |
   +-------------------------+----------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`bool<class_bool_constructor_bool>`\ (\ from\: :ref:`float<class_float>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`bool<class_bool_constructor_bool>`\ (\ from\: :ref:`int<class_int>`\ )     |
   +-------------------------+----------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Operators
---------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator !=<class_bool_operator_neq_bool>`\ (\ right\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator \<<class_bool_operator_lt_bool>`\ (\ right\: :ref:`bool<class_bool>`\ )  |
   +-------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator ==<class_bool_operator_eq_bool>`\ (\ right\: :ref:`bool<class_bool>`\ )  |
   +-------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`operator ><class_bool_operator_gt_bool>`\ (\ right\: :ref:`bool<class_bool>`\ )   |
   +-------------------------+-----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả constructor
-----------------

.. _class_bool_constructor_bool:

.. rst-class:: classref-constructor

:ref:`bool<class_bool>` **bool**\ (\ ) :ref:`🔗<class_bool_constructor_bool>`

Tạo một **bool** được đặt thành ``false``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`bool<class_bool>` **bool**\ (\ from\: :ref:`bool<class_bool>`\ )

Tạo một **bool** dưới dạng bản sao của **bool** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`bool<class_bool>` **bool**\ (\ from\: :ref:`float<class_float>`\ )

Ép kiểu một giá trị :ref:`float<class_float>` thành **bool**. Trả về ``false`` nếu ``from`` bằng ``0.0`` (bao gồm cả ``-0.0``), và ``true`` cho mọi giá trị khác (bao gồm cả :ref:`@GDScript.INF<class_@GDScript_constant_INF>` và :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>`).

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`bool<class_bool>` **bool**\ (\ from\: :ref:`int<class_int>`\ )

Ép kiểu một giá trị :ref:`int<class_int>` thành **bool**. Trả về ``false`` nếu ``from`` bằng ``0``, và ``true`` cho mọi giá trị khác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_bool_operator_neq_bool:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_bool_operator_neq_bool>`

Trả về ``true`` nếu một **bool** là ``true`` và **bool** còn lại là ``false``. Tương đương với XOR logic (NEQ).

.. rst-class:: classref-item-separator

----

.. _class_bool_operator_lt_bool:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_bool_operator_lt_bool>`

Trả về ``true`` nếu **bool** bên trái là ``false`` và ``right`` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_bool_operator_eq_bool:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_bool_operator_eq_bool>`

Trả về ``true`` nếu cả hai **bool**\ s đều là ``true``, hoặc nếu cả hai **bool**\ s đều là ``false``. Tương đương với XNOR logic (EQ).

.. rst-class:: classref-item-separator

----

.. _class_bool_operator_gt_bool:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_bool_operator_gt_bool>`

Trả về ``true`` nếu **bool** bên trái là ``true`` và ``right`` là ``false``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
