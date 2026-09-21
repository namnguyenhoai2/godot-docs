:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MainLoop.xml.

.. _class_MainLoop:

MainLoop
========

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`SceneTree<class_SceneTree>`

Lớp cơ sở trừu tượng cho main loop của game.

.. rst-class:: classref-introduction-group

Mô tả
-----

**MainLoop** là lớp cơ sở trừu tượng cho game loop của một dự án Godot. Lớp này được :ref:`SceneTree<class_SceneTree>` kế thừa, đây là triển khai game loop mặc định được sử dụng trong các dự án Godot, mặc dù bạn cũng có thể tự viết và sử dụng một subclass **MainLoop** của riêng mình thay cho scene tree.

Khi ứng dụng khởi động, phải cung cấp một triển khai **MainLoop** cho OS; nếu không, ứng dụng sẽ thoát. Việc này diễn ra tự động (và một :ref:`SceneTree<class_SceneTree>` được tạo) trừ khi một **MainLoop** :ref:`Script<class_Script>` được cung cấp từ command line (ví dụ với ``godot -s my_loop.gd``) hoặc thiết lập project :ref:`ProjectSettings.application/run/main_loop_type<class_ProjectSettings_property_application/run/main_loop_type>` bị ghi đè.

Sau đây là một script ví dụ triển khai **MainLoop** đơn giản:


.. tabs::

 .. code-tab:: gdscript

    class_name CustomMainLoop
    extends MainLoop

    var time_elapsed = 0

    func _initialize():
        print("Initialized:")
        print("  Starting time: %s" % str(time_elapsed))

    func _process(delta):
        time_elapsed += delta
        # Trả về true để kết thúc main loop.
        return Input.get_mouse_button_mask() != 0 || Input.is_key_pressed(KEY_ESCAPE)

    func _finalize():
        print("Finalized:")
        print("  End time: %s" % str(time_elapsed))

 .. code-tab:: csharp

    using Godot;

    [GlobalClass]
    public partial class CustomMainLoop : MainLoop
    {
        private double _timeElapsed = 0;

        public override void _Initialize()
        {
            GD.Print("Initialized:");
            GD.Print($"  Starting Time: {_timeElapsed}");
        }

        public override bool _Process(double delta)
        {
            _timeElapsed += delta;
            // Trả về true để kết thúc main loop.
            return Input.GetMouseButtonMask() != 0 || Input.IsKeyPressed(Key.Escape);
        }

        private void _Finalize()
        {
            GD.Print("Finalized:");
            GD.Print($"  End Time: {_timeElapsed}");
        }
    }



.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_finalize<class_MainLoop_private_method__finalize>`\ (\ ) |virtual|                                                  |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_initialize<class_MainLoop_private_method__initialize>`\ (\ ) |virtual|                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`_physics_process<class_MainLoop_private_method__physics_process>`\ (\ delta\: :ref:`float<class_float>`\ ) |virtual| |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`_process<class_MainLoop_private_method__process>`\ (\ delta\: :ref:`float<class_float>`\ ) |virtual|                 |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_MainLoop_signal_on_request_permissions_result:

.. rst-class:: classref-signal

**on_request_permissions_result**\ (\ permission\: :ref:`String<class_String>`, granted\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_MainLoop_signal_on_request_permissions_result>`

Được phát ra khi người dùng phản hồi một yêu cầu cấp quyền.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_MainLoop_constant_NOTIFICATION_OS_MEMORY_WARNING:

.. rst-class:: classref-constant

**NOTIFICATION_OS_MEMORY_WARNING** = ``2009`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_OS_MEMORY_WARNING>`

Thông báo nhận được từ OS khi ứng dụng vượt quá dung lượng bộ nhớ được cấp.

Chỉ dành cho nền tảng iOS.

.. _class_MainLoop_constant_NOTIFICATION_TRANSLATION_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_TRANSLATION_CHANGED** = ``2010`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_TRANSLATION_CHANGED>`

Thông báo nhận được khi các bản dịch có thể đã thay đổi. Có thể được kích hoạt khi người dùng thay đổi locale. Có thể được sử dụng để phản hồi các thay đổi về ngôn ngữ, chẳng hạn như thay đổi các chuỗi UI ngay lập tức. Hữu ích khi làm việc với hỗ trợ translation tích hợp sẵn, như :ref:`Object.tr()<class_Object_method_tr>`.

.. _class_MainLoop_constant_NOTIFICATION_WM_ABOUT:

.. rst-class:: classref-constant

**NOTIFICATION_WM_ABOUT** = ``2011`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_WM_ABOUT>`

Thông báo nhận được từ OS khi có yêu cầu cung cấp thông tin "About".

Chỉ dành cho nền tảng macOS.

.. _class_MainLoop_constant_NOTIFICATION_CRASH:

.. rst-class:: classref-constant

**NOTIFICATION_CRASH** = ``2012`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_CRASH>`

Thông báo nhận được từ crash handler của Godot khi engine sắp gặp sự cố.

Được triển khai trên các nền tảng desktop nếu crash handler được bật.

.. _class_MainLoop_constant_NOTIFICATION_OS_IME_UPDATE:

.. rst-class:: classref-constant

**NOTIFICATION_OS_IME_UPDATE** = ``2013`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_OS_IME_UPDATE>`

Thông báo nhận được từ OS khi Input Method Engine được cập nhật (ví dụ: thay đổi vị trí con trỏ IME hoặc chuỗi composition).

Được triển khai trên các nền tảng desktop và web.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_RESUMED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_RESUMED** = ``2014`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_RESUMED>`

Thông báo nhận được từ OS khi ứng dụng được tiếp tục.

Chỉ dành cho các nền tảng Android và iOS.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_PAUSED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PAUSED** = ``2015`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_PAUSED>`

Thông báo nhận được từ OS khi ứng dụng bị tạm dừng.

Chỉ dành cho các nền tảng Android và iOS.

\ **Lưu ý:** Trên iOS, bạn chỉ có khoảng 5 giây để hoàn tất một tác vụ được bắt đầu bởi signal này. Nếu vượt quá khoảng thời gian đó, iOS sẽ buộc app thoát thay vì tạm dừng app.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_FOCUS_IN:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_FOCUS_IN** = ``2016`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_FOCUS_IN>`

Thông báo nhận được từ OS khi ứng dụng được focus, tức là khi chuyển focus từ desktop của OS hoặc một ứng dụng bên thứ ba sang bất kỳ cửa sổ đang mở nào của instance Godot.

Được triển khai trên các nền tảng desktop và mobile.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_FOCUS_OUT:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_FOCUS_OUT** = ``2017`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_FOCUS_OUT>`

Thông báo nhận được từ OS khi ứng dụng mất focus, tức là khi chuyển focus từ bất kỳ cửa sổ đang mở nào của instance Godot sang desktop của OS hoặc một ứng dụng bên thứ ba.

Được triển khai trên các nền tảng desktop và mobile.

.. _class_MainLoop_constant_NOTIFICATION_TEXT_SERVER_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_TEXT_SERVER_CHANGED** = ``2018`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_TEXT_SERVER_CHANGED>`

Thông báo nhận được khi text server thay đổi.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_PIP_MODE_ENTERED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PIP_MODE_ENTERED** = ``2019`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_PIP_MODE_ENTERED>`

Thông báo nhận được khi ứng dụng chuyển sang chế độ picture-in-picture.

.. _class_MainLoop_constant_NOTIFICATION_APPLICATION_PIP_MODE_EXITED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PIP_MODE_EXITED** = ``2020`` :ref:`🔗<class_MainLoop_constant_NOTIFICATION_APPLICATION_PIP_MODE_EXITED>`

Thông báo nhận được khi ứng dụng thoát khỏi chế độ picture-in-picture.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_MainLoop_private_method__finalize:

.. rst-class:: classref-method

|void| **_finalize**\ (\ ) |virtual| :ref:`🔗<class_MainLoop_private_method__finalize>`

Được gọi trước khi chương trình thoát.

.. rst-class:: classref-item-separator

----

.. _class_MainLoop_private_method__initialize:

.. rst-class:: classref-method

|void| **_initialize**\ (\ ) |virtual| :ref:`🔗<class_MainLoop_private_method__initialize>`

Được gọi một lần trong quá trình khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_MainLoop_private_method__physics_process:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_physics_process**\ (\ delta\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_MainLoop_private_method__physics_process>`

Được gọi ở mỗi physics tick. ``delta`` là thời gian logic giữa các physics tick, tính bằng giây, và bằng :ref:`Engine.time_scale<class_Engine_property_time_scale>` / :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`. Tương đương với :ref:`Node._physics_process()<class_Node_private_method__physics_process>`.

Nếu được triển khai, phương thức này phải trả về một giá trị boolean. ``true`` kết thúc main loop, còn ``false`` cho phép main loop tiếp tục sang bước kế tiếp.

\ **Lưu ý:** :ref:`_physics_process()<class_MainLoop_private_method__physics_process>` có thể được gọi tối đa :ref:`Engine.max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` lần trong mỗi frame (idle). Giới hạn bước này có thể đạt được khi engine đang gặp vấn đề về hiệu năng.

\ **Lưu ý:** ``delta`` tích lũy có thể lệch so với số giây trong thế giới thực.

.. rst-class:: classref-item-separator

----

.. _class_MainLoop_private_method__process:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_process**\ (\ delta\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_MainLoop_private_method__process>`

Được gọi ở mỗi idle frame, trước khi render và sau khi các physics tick đã được xử lý. ``delta`` là khoảng thời gian giữa các frame, tính bằng giây. Tương đương với :ref:`Node._process()<class_Node_private_method__process>`.

Nếu được triển khai, phương thức này phải trả về một giá trị boolean. ``true`` kết thúc main loop, còn ``false`` cho phép main loop tiếp tục sang frame kế tiếp.

\ **Lưu ý:** Khi engine gặp khó khăn và frame rate giảm, ``delta`` sẽ tăng. Khi ``delta`` tăng, giá trị này bị giới hạn ở mức tối đa :ref:`Engine.time_scale<class_Engine_property_time_scale>` \* :ref:`Engine.max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` / :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`. Do đó, ``delta`` tích lũy có thể không đại diện cho thời gian thực.

\ **Lưu ý:** Khi ``--fixed-fps`` được bật hoặc engine đang chạy ở Movie Maker mode (xem :ref:`MovieWriter<class_MovieWriter>`), process ``delta`` sẽ luôn giống nhau ở mọi frame, bất kể frame mất bao lâu để render.

\ **Lưu ý:** Delta của frame có thể được hậu xử lý bởi :ref:`OS.delta_smoothing<class_OS_property_delta_smoothing>` nếu tính năng này được bật cho project.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
