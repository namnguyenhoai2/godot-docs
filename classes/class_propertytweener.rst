:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PropertyTweener.xml.

.. _class_PropertyTweener:

PropertyTweener
===============

**Kế thừa:** :ref:`Tweener<class_Tweener>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Nội suy thuộc tính của :ref:`Object<class_Object>` theo thời gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PropertyTweener** được dùng để nội suy một thuộc tính trong một đối tượng. Xem :ref:`Tween.tween_property()<class_Tween_method_tween_property>` để biết thêm thông tin về cách sử dụng.

Tweener sẽ tự động hoàn tất nếu đối tượng đích được giải phóng.

\ **Lưu ý:** :ref:`Tween.tween_property()<class_Tween_method_tween_property>` là cách duy nhất đúng để tạo **PropertyTweener**. Bất kỳ **PropertyTweener** nào được tạo thủ công sẽ không hoạt động chính xác.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`as_relative<class_PropertyTweener_method_as_relative>`\ (\ )                                                                                |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`from<class_PropertyTweener_method_from>`\ (\ value\: :ref:`Variant<class_Variant>`\ )                                                       |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`from_current<class_PropertyTweener_method_from_current>`\ (\ )                                                                              |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`set_custom_interpolator<class_PropertyTweener_method_set_custom_interpolator>`\ (\ interpolator_method\: :ref:`Callable<class_Callable>`\ ) |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`set_delay<class_PropertyTweener_method_set_delay>`\ (\ delay\: :ref:`float<class_float>`\ )                                                 |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`set_ease<class_PropertyTweener_method_set_ease>`\ (\ ease\: :ref:`EaseType<enum_Tween_EaseType>`\ )                                         |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PropertyTweener<class_PropertyTweener>` | :ref:`set_trans<class_PropertyTweener_method_set_trans>`\ (\ trans\: :ref:`TransitionType<enum_Tween_TransitionType>`\ )                          |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PropertyTweener_method_as_relative:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **as_relative**\ (\ ) :ref:`🔗<class_PropertyTweener_method_as_relative>`

Khi được gọi, giá trị cuối sẽ được sử dụng thay vào đó như một giá trị tương đối.

\ **Ví dụ:** Di chuyển node sang phải ``100`` pixel.


.. tabs::

 .. code-tab:: gdscript

    var tween = get_tree().create_tween()
    tween.tween_property(self, "position", Vector2.RIGHT * 100, 1).as_relative()

 .. code-tab:: csharp

    Tween tween = GetTree().CreateTween();
    tween.TweenProperty(this, "position", Vector2.Right * 100.0f, 1.0f).AsRelative();



.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_from:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **from**\ (\ value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_PropertyTweener_method_from>`

Đặt giá trị ban đầu tùy chỉnh cho **PropertyTweener**.

\ **Ví dụ:** Di chuyển node từ vị trí ``(100, 100)`` đến ``(200, 100)``.


.. tabs::

 .. code-tab:: gdscript

    var tween = get_tree().create_tween()
    tween.tween_property(self, "position", Vector2(200, 100), 1).from(Vector2(100, 100))

 .. code-tab:: csharp

    Tween tween = GetTree().CreateTween();
    tween.TweenProperty(this, "position", new Vector2(200.0f, 100.0f), 1.0f).From(new Vector2(100.0f, 100.0f));



.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_from_current:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **from_current**\ (\ ) :ref:`🔗<class_PropertyTweener_method_from_current>`

Khiến **PropertyTweener** sử dụng giá trị thuộc tính hiện tại (tức là tại thời điểm tạo **PropertyTweener** này) làm điểm bắt đầu. Điều này tương đương với việc sử dụng :ref:`from()<class_PropertyTweener_method_from>` cùng giá trị hiện tại. Hai lệnh gọi này sẽ thực hiện cùng một việc:


.. tabs::

 .. code-tab:: gdscript

    tween.tween_property(self, "position", Vector2(200, 100), 1).from(position)
    tween.tween_property(self, "position", Vector2(200, 100), 1).from_current()

 .. code-tab:: csharp

    tween.TweenProperty(this, "position", new Vector2(200.0f, 100.0f), 1.0f).From(Position);
    tween.TweenProperty(this, "position", new Vector2(200.0f, 100.0f), 1.0f).FromCurrent();



.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_set_custom_interpolator:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **set_custom_interpolator**\ (\ interpolator_method\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_PropertyTweener_method_set_custom_interpolator>`

Cho phép nội suy giá trị bằng một hàm easing tùy chỉnh. ``interpolator_method`` được cung cấp sẽ được gọi với một giá trị nằm trong khoảng từ ``0.0`` đến ``1.0`` và được kỳ vọng trả về một giá trị trong cùng khoảng đó (có thể sử dụng các giá trị nằm ngoài khoảng để tạo hiệu ứng overshoot). Giá trị trả về của phương thức sau đó được sử dụng để nội suy giữa giá trị ban đầu và giá trị cuối. Lưu ý rằng tham số được truyền cho phương thức vẫn chịu ảnh hưởng của easing riêng của tweener.


.. tabs::

 .. code-tab:: gdscript

    @export var curve: Curve

    func _ready():
        var tween = create_tween()
        # Nội suy giá trị bằng một curve tùy chỉnh.
        tween.tween_property(self, "position:x", 300, 1).as_relative().set_custom_interpolator(tween_curve)

    func tween_curve(v):
        return curve.sample_baked(v)

 .. code-tab:: csharp

    [Export]
    public Curve Curve { get; set; }

    public override void _Ready()
    {
        Tween tween = CreateTween();
        // Nội suy giá trị bằng một curve tùy chỉnh.
        Callable tweenCurveCallable = Callable.From<float, float>(TweenCurve);
        tween.TweenProperty(this, "position:x", 300.0f, 1.0f).AsRelative().SetCustomInterpolator(tweenCurveCallable);
    }

    private float TweenCurve(float value)
    {
        return Curve.SampleBaked(value);
    }



.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_set_delay:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **set_delay**\ (\ delay\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PropertyTweener_method_set_delay>`

Đặt thời gian tính bằng giây sau đó **PropertyTweener** sẽ bắt đầu nội suy. Theo mặc định, không có độ trễ.

.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_set_ease:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **set_ease**\ (\ ease\: :ref:`EaseType<enum_Tween_EaseType>`\ ) :ref:`🔗<class_PropertyTweener_method_set_ease>`

Đặt loại easing được sử dụng từ :ref:`EaseType<enum_Tween_EaseType>`. Nếu không được đặt, easing mặc định từ :ref:`Tween<class_Tween>` chứa Tweener này sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_PropertyTweener_method_set_trans:

.. rst-class:: classref-method

:ref:`PropertyTweener<class_PropertyTweener>` **set_trans**\ (\ trans\: :ref:`TransitionType<enum_Tween_TransitionType>`\ ) :ref:`🔗<class_PropertyTweener_method_set_trans>`

Đặt loại transition được sử dụng từ :ref:`TransitionType<enum_Tween_TransitionType>`. Nếu không được đặt, transition mặc định từ :ref:`Tween<class_Tween>` chứa Tweener này sẽ được sử dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
