:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CompressedTexture3D.xml.

.. _class_CompressedTexture3D:

CompressedTexture3D
===================

**Kế thừa:** :ref:`Texture3D<class_Texture3D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture có 3 chiều, có thể được nén.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CompressedTexture3D** là phiên bản tương ứng được nén VRAM của :ref:`ImageTexture3D<class_ImageTexture3D>`. Phần mở rộng tệp của các tệp **CompressedTexture3D** là ``.ctex3d``. Định dạng tệp này là định dạng nội bộ của Godot; nó được tạo bằng cách import các định dạng hình ảnh khác thông qua hệ thống import.

\ **CompressedTexture3D** sử dụng tính năng nén VRAM, cho phép giảm mức sử dụng bộ nhớ trên GPU khi render texture. Điều này cũng cải thiện thời gian tải, vì các texture được nén VRAM tải nhanh hơn so với các texture sử dụng tính năng nén không mất dữ liệu. Nén VRAM có thể tạo ra các artifact dễ nhận thấy và được thiết kế để sử dụng cho việc render 3D, không phải 2D.

Xem :ref:`Texture3D<class_Texture3D>` để biết mô tả tổng quan về texture 3D.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+----------------------------------------------------------------+--------+
   | :ref:`String<class_String>` | :ref:`load_path<class_CompressedTexture3D_property_load_path>` | ``""`` |
   +-----------------------------+----------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load<class_CompressedTexture3D_method_load>`\ (\ path\: :ref:`String<class_String>`\ ) |
   +---------------------------------------+----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CompressedTexture3D_property_load_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **load_path** = ``""`` :ref:`🔗<class_CompressedTexture3D_property_load_path>`

.. rst-class:: classref-property-setget

- :ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_load_path**\ (\ )

Đường dẫn tệp của **CompressedTexture3D** đến tệp ``.ctex3d``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CompressedTexture3D_method_load:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_CompressedTexture3D_method_load>`

Tải texture từ ``path`` được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
