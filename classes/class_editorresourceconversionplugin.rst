:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorResourceConversionPlugin.xml.

.. _class_EditorResourceConversionPlugin:

EditorResourceConversionPlugin
==============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Plugin để thêm các bộ chuyển đổi tùy chỉnh từ định dạng resource này sang định dạng resource khác trong menu ngữ cảnh của resource picker trong editor; ví dụ: chuyển đổi một :ref:`StandardMaterial3D<class_StandardMaterial3D>` thành một :ref:`ShaderMaterial<class_ShaderMaterial>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorResourceConversionPlugin** được gọi khi menu ngữ cảnh được mở cho một resource trong editor inspector. Các plugin chuyển đổi phù hợp sẽ xuất hiện dưới dạng tùy chọn menu để chuyển đổi resource đã cho sang một kiểu đích.

Dưới đây là ví dụ về một plugin cơ bản có thể chuyển đổi một :ref:`ImageTexture<class_ImageTexture>` thành một :ref:`PortableCompressedTexture2D<class_PortableCompressedTexture2D>`.


.. tabs::

 .. code-tab:: gdscript

    extends EditorResourceConversionPlugin

    func _handles(resource: Resource):
        return resource is ImageTexture

    func _converts_to():
        return "PortableCompressedTexture2D"

    func _convert(itex: Resource):
        var ptex = PortableCompressedTexture2D.new()
        ptex.create_from_image(itex.get_image(), PortableCompressedTexture2D.COMPRESSION_MODE_LOSSLESS)
        return ptex



Để sử dụng **EditorResourceConversionPlugin**, trước tiên hãy đăng ký plugin bằng phương thức :ref:`EditorPlugin.add_resource_conversion_plugin()<class_EditorPlugin_method_add_resource_conversion_plugin>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>` | :ref:`_convert<class_EditorResourceConversionPlugin_private_method__convert>`\ (\ resource\: :ref:`Resource<class_Resource>`\ ) |virtual| |const| |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`     | :ref:`_converts_to<class_EditorResourceConversionPlugin_private_method__converts_to>`\ (\ ) |virtual| |const|                                     |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`_handles<class_EditorResourceConversionPlugin_private_method__handles>`\ (\ resource\: :ref:`Resource<class_Resource>`\ ) |virtual| |const| |
   +---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorResourceConversionPlugin_private_method__convert:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **_convert**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) |virtual| |const| :ref:`🔗<class_EditorResourceConversionPlugin_private_method__convert>`

Nhận một :ref:`Resource<class_Resource>` đầu vào và chuyển đổi nó thành kiểu được chỉ định trong :ref:`_converts_to()<class_EditorResourceConversionPlugin_private_method__converts_to>`. :ref:`Resource<class_Resource>` được trả về là kết quả của quá trình chuyển đổi, còn :ref:`Resource<class_Resource>` đầu vào vẫn không thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourceConversionPlugin_private_method__converts_to:

.. rst-class:: classref-method

:ref:`String<class_String>` **_converts_to**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorResourceConversionPlugin_private_method__converts_to>`

Trả về tên lớp của kiểu đích của :ref:`Resource<class_Resource>` mà plugin này chuyển đổi các resource nguồn sang.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourceConversionPlugin_private_method__handles:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_handles**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) |virtual| |const| :ref:`🔗<class_EditorResourceConversionPlugin_private_method__handles>`

Được gọi để xác định xem một :ref:`Resource<class_Resource>` cụ thể có thể được plugin này chuyển đổi sang kiểu resource đích hay không.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
