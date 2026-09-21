:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRFutureExtension.xml.

.. _class_OpenXRFutureExtension:

OpenXRFutureExtension
=====================

**Kế thừa:** :ref:`OpenXRExtensionWrapper<class_OpenXRExtensionWrapper>` **<** :ref:`Object<class_Object>`

Extension OpenXR Future cho phép sử dụng các API bất đồng bộ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một extension hỗ trợ trong OpenXR, cho phép các extension OpenXR khác khởi chạy các hàm bất đồng bộ và nhận callback sau khi hàm đó hoàn tất. Extension này không предназнач cho việc sử dụng trong GDScript nhưng có thể được truy cập từ GDExtension.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`cancel_future<class_OpenXRFutureExtension_method_cancel_future>`\ (\ future\: :ref:`int<class_int>`\ )                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_active<class_OpenXRFutureExtension_method_is_active>`\ (\ ) |const|                                                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` | :ref:`register_future<class_OpenXRFutureExtension_method_register_future>`\ (\ future\: :ref:`int<class_int>`, on_success\: :ref:`Callable<class_Callable>` = Callable()\ ) |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_OpenXRFutureExtension_method_cancel_future:

.. rst-class:: classref-method

|void| **cancel_future**\ (\ future\: :ref:`int<class_int>`\ ) :ref:`🔗<class_OpenXRFutureExtension_method_cancel_future>`

Hủy một future đang chạy. ``future`` phải là một giá trị ``XrFutureEXT`` được API khởi chạy một hàm bất đồng bộ trả về trước đó.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRFutureExtension_method_is_active:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_active**\ (\ ) |const| :ref:`🔗<class_OpenXRFutureExtension_method_is_active>`

Trả về ``true`` nếu runtime OpenXR đang được sử dụng có các future khả dụng. Hàm này chỉ trả về một kết quả có thể sử dụng sau khi OpenXR đã được khởi tạo.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRFutureExtension_method_register_future:

.. rst-class:: classref-method

:ref:`OpenXRFutureResult<class_OpenXRFutureResult>` **register_future**\ (\ future\: :ref:`int<class_int>`, on_success\: :ref:`Callable<class_Callable>` = Callable()\ ) :ref:`🔗<class_OpenXRFutureExtension_method_register_future>`

Đăng ký một đối tượng OpenXR Future để chúng ta theo dõi việc hoàn tất. ``future`` phải là một giá trị ``XrFutureEXT`` được API khởi chạy một hàm bất đồng bộ trả về trước đó.

Bạn có thể tùy chọn chỉ định ``on_success``; nó sẽ được gọi khi future hoàn tất thành công.

Hoặc bạn có thể sử dụng đối tượng :ref:`OpenXRFutureResult<class_OpenXRFutureResult>` được trả về để ``await`` signal :ref:`OpenXRFutureResult.completed<class_OpenXRFutureResult_signal_completed>` của đối tượng đó.

::

    var future_result = OpenXRFutureExtension.register_future(future)
    await future_result.completed
    if future_result.get_status() == OpenXRFutureResult.RESULT_FINISHED:
        # Xử lý trường hợp thành công
        pass

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
