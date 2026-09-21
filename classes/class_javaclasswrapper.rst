:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/JavaClassWrapper.xml.

.. _class_JavaClassWrapper:

JavaClassWrapper
================

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào Java Native Interface.

.. rst-class:: classref-introduction-group

Mô tả
-----

Singleton JavaClassWrapper cung cấp cách để ứng dụng Godot gửi và nhận dữ liệu thông qua `Java Native Interface <https://developer.android.com/training/articles/perf-jni>`__ (JNI).

\ **Lưu ý:** Singleton này chỉ khả dụng trong các bản build Android.

::

    var LocalDateTime = JavaClassWrapper.wrap("java.time.LocalDateTime")
    var DateTimeFormatter = JavaClassWrapper.wrap("java.time.format.DateTimeFormatter")

    var datetime = LocalDateTime.now()
    var formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss")

    print(datetime.format(formatter))

\ **Cảnh báo:** Khi gọi các phương thức Java, hãy nhớ kiểm tra :ref:`get_exception()<class_JavaClassWrapper_method_get_exception>` để xác định xem phương thức có phát sinh exception hay không.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Tích hợp với các API Android <../tutorials/platform/android/javaclasswrapper_and_androidruntimeplugin>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaObject<class_JavaObject>` | :ref:`create_proxy<class_JavaClassWrapper_method_create_proxy>`\ (\ object\: :ref:`Object<class_Object>`, interfaces\: :ref:`PackedStringArray<class_PackedStringArray>`\ )  |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaObject<class_JavaObject>` | :ref:`create_sam_callback<class_JavaClassWrapper_method_create_sam_callback>`\ (\ sam_interface\: :ref:`String<class_String>`, callable\: :ref:`Callable<class_Callable>`\ ) |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaObject<class_JavaObject>` | :ref:`get_exception<class_JavaClassWrapper_method_get_exception>`\ (\ )                                                                                                      |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaClass<class_JavaClass>`   | :ref:`wrap<class_JavaClassWrapper_method_wrap>`\ (\ name\: :ref:`String<class_String>`\ )                                                                                    |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_JavaClassWrapper_method_create_proxy:

.. rst-class:: classref-method

:ref:`JavaObject<class_JavaObject>` **create_proxy**\ (\ object\: :ref:`Object<class_Object>`, interfaces\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_JavaClassWrapper_method_create_proxy>`

Tạo một :ref:`JavaObject<class_JavaObject>` triển khai các interface Java đã cho, sử dụng :ref:`Object<class_Object>` đã cho làm phần triển khai.

``object`` phải chứa các chữ ký phương thức khớp với chữ ký của các phương thức từ Java ``interfaces`` được truyền vào. Việc gọi các phương thức từ Java ``interfaces`` sẽ chuyển đến phương thức ``object`` tương ứng.

::

    class PrintProxy:
        func println(content: String) -> void:
            print(content)

    var print_proxy = PrintProxy.new()
    var printer_object = JavaClassWrapper.create_proxy(print_proxy, ["android.util.Printer"])
    printer_object.println("Hello Godot World!")

\ **Lưu ý:** Phương thức này chỉ hoạt động trên Android. Trên mọi nền tảng khác, phương thức này sẽ luôn trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_JavaClassWrapper_method_create_sam_callback:

.. rst-class:: classref-method

:ref:`JavaObject<class_JavaObject>` **create_sam_callback**\ (\ sam_interface\: :ref:`String<class_String>`, callable\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_JavaClassWrapper_method_create_sam_callback>`

Tạo một :ref:`JavaObject<class_JavaObject>` triển khai interface Java Single Abstract Method (SAM), sử dụng :ref:`Callable<class_Callable>` của Godot làm phần triển khai.

``sam_interface`` **phải** là một interface Java SAM, nghĩa là nó chỉ được có một abstract method để triển khai.

``callable`` phải có khả năng xử lý các kiểu tham số giống như phương thức của interface SAM và phải cung cấp cùng kiểu trả về. ``callable`` sẽ được gọi dưới dạng callback, với các đối số được truyền từ phương thức của interface Java SAM.

::

    var cb = func (content: String) -> void:
        print(content)
    var callback = JavaClassWrapper.create_sam_callback("android.util.Printer", cb)
    callback.println("Hello Godot World!")

\ **Lưu ý:** Phương thức này chỉ hoạt động trên Android. Trên mọi nền tảng khác, phương thức này sẽ luôn trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_JavaClassWrapper_method_get_exception:

.. rst-class:: classref-method

:ref:`JavaObject<class_JavaObject>` **get_exception**\ (\ ) :ref:`🔗<class_JavaClassWrapper_method_get_exception>`

Trả về exception Java từ lần gọi gần nhất vào một class Java. Nếu không có exception, phương thức sẽ trả về ``null``.

\ **Lưu ý:** Phương thức này chỉ hoạt động trên Android. Trên mọi nền tảng khác, phương thức này sẽ luôn trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_JavaClassWrapper_method_wrap:

.. rst-class:: classref-method

:ref:`JavaClass<class_JavaClass>` **wrap**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_JavaClassWrapper_method_wrap>`

Bọc một class được định nghĩa trong Java và trả về class đó dưới dạng kiểu :ref:`JavaClass<class_JavaClass>` :ref:`Object<class_Object>` mà Godot có thể tương tác.

Khi bọc các class bên trong (nested), hãy sử dụng ``Khi bọc các class bên trong (nested), hãy sử dụng ` thay cho ``.`` để phân tách chúng. Ví dụ, ``JavaClassWrapper.wrap("android.view.WindowManager$LayoutParams")`` bọc class **WindowManager.LayoutParams**.

\ **Lưu ý:** Để gọi một constructor, hãy gọi một phương thức có cùng tên với class. Ví dụ:

::

    var Intent = JavaClassWrapper.wrap("android.content.Intent")
    var intent = Intent.Intent()

\ **Lưu ý:** Phương thức này chỉ hoạt động trên Android. Trên mọi nền tảng khác, phương thức này không thực hiện thao tác nào và trả về một :ref:`JavaClass<class_JavaClass>` rỗng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
