:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/JavaScriptObject.xml.

.. _class_JavaScriptObject:

JavaScriptObject
================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một lớp wrapper cho các đối tượng JavaScript native trên web.

.. rst-class:: classref-introduction-group

Mô tả
-----

JavaScriptObject được dùng để tương tác với các đối tượng JavaScript được truy xuất hoặc tạo thông qua :ref:`JavaScriptBridge.get_interface()<class_JavaScriptBridge_method_get_interface>`, :ref:`JavaScriptBridge.create_object()<class_JavaScriptBridge_method_create_object>` hoặc :ref:`JavaScriptBridge.create_callback()<class_JavaScriptBridge_method_create_callback>`.

::

    extends Node

    var _my_js_callback = JavaScriptBridge.create_callback(myCallback) # Phải giữ tham chiếu này
    var console = JavaScriptBridge.get_interface("console")

    func _init():
        var buf = JavaScriptBridge.create_object("ArrayBuffer", 10) # new ArrayBuffer(10)
        print(buf) # In ra [JavaScriptObject:OBJECT_ID]
        var uint8arr = JavaScriptBridge.create_object("Uint8Array", buf) # new Uint8Array(buf)
        uint8arr[1] = 255
        prints(uint8arr[1], uint8arr.byteLength) # In ra "255 10"

        # In ra "Uint8Array(10) [ 0, 255, 0, 0, 0, 0, 0, 0, 0, 0 ]" trong console của trình duyệt.
        console.log(uint8arr)

        # Tương đương với JavaScriptBridge: Array.from(uint8arr).forEach(myCallback)
        JavaScriptBridge.get_interface("Array").from(uint8arr).forEach(_my_js_callback)

    func myCallback(args):
        # Sẽ được gọi với các tham số được truyền vào callback "forEach"
        # [0, 0, [JavaScriptObject:1173]]
        # [255, 1, [JavaScriptObject:1173]]
        # ...
        # [0, 9, [JavaScriptObject:1180]]
        print(args)

\ **Lưu ý:** Chỉ khả dụng trên nền tảng Web.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
