:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BackBufferCopy.xml.

.. _class_BackBufferCopy:

BackBufferCopy
==============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node sao chép một vùng trên màn hình vào một bộ đệm để truy cập trong mã shader.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node dùng để lưu màn hình hiện đang hiển thị vào back-buffer. Vùng được xác định trong node **BackBufferCopy** sẽ được lưu vào bộ đệm cùng với nội dung của phần màn hình mà nó bao phủ, hoặc toàn bộ màn hình tùy theo :ref:`copy_mode<class_BackBufferCopy_property_copy_mode>`. Có thể truy cập vùng này trong các shader script bằng screen texture (tức là một uniform sampler với ``hint_screen_texture``).

\ **Lưu ý:** Vì node này kế thừa từ :ref:`Node2D<class_Node2D>` (chứ không phải :ref:`Control<class_Control>`), anchors và margins sẽ không được áp dụng cho các node con dẫn xuất từ :ref:`Control<class_Control>`. Điều này có thể gây ra vấn đề khi thay đổi kích thước cửa sổ. Để tránh vấn đề này, hãy thêm các node dẫn xuất từ :ref:`Control<class_Control>` dưới dạng *anh em* với node **BackBufferCopy**, thay vì thêm chúng làm node con.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Shader đọc màn hình <../tutorials/shaders/screen-reading_shaders>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------+-----------------------------------------------------------+---------------------------------+
   | :ref:`CopyMode<enum_BackBufferCopy_CopyMode>` | :ref:`copy_mode<class_BackBufferCopy_property_copy_mode>` | ``1``                           |
   +-----------------------------------------------+-----------------------------------------------------------+---------------------------------+
   | :ref:`Rect2<class_Rect2>`                     | :ref:`rect<class_BackBufferCopy_property_rect>`           | ``Rect2(-100, -100, 200, 200)`` |
   +-----------------------------------------------+-----------------------------------------------------------+---------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các giá trị enum
----------------

.. _enum_BackBufferCopy_CopyMode:

.. rst-class:: classref-enumeration

enum **CopyMode**: :ref:`🔗<enum_BackBufferCopy_CopyMode>`

.. _class_BackBufferCopy_constant_COPY_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`CopyMode<enum_BackBufferCopy_CopyMode>` **COPY_MODE_DISABLED** = ``0``

Tắt chế độ buffering. Điều này có nghĩa là node **BackBufferCopy** sẽ trực tiếp sử dụng phần màn hình mà nó bao phủ.

.. _class_BackBufferCopy_constant_COPY_MODE_RECT:

.. rst-class:: classref-enumeration-constant

:ref:`CopyMode<enum_BackBufferCopy_CopyMode>` **COPY_MODE_RECT** = ``1``

**BackBufferCopy** lưu một vùng hình chữ nhật vào bộ đệm.

.. _class_BackBufferCopy_constant_COPY_MODE_VIEWPORT:

.. rst-class:: classref-enumeration-constant

:ref:`CopyMode<enum_BackBufferCopy_CopyMode>` **COPY_MODE_VIEWPORT** = ``2``

**BackBufferCopy** lưu toàn bộ màn hình vào bộ đệm.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BackBufferCopy_property_copy_mode:

.. rst-class:: classref-property

:ref:`CopyMode<enum_BackBufferCopy_CopyMode>` **copy_mode** = ``1`` :ref:`🔗<class_BackBufferCopy_property_copy_mode>`

.. rst-class:: classref-property-setget

- |void| **set_copy_mode**\ (\ value\: :ref:`CopyMode<enum_BackBufferCopy_CopyMode>`\ ) - :ref:`CopyMode<enum_BackBufferCopy_CopyMode>` **get_copy_mode**\ (\ )

Chế độ bộ đệm.

.. rst-class:: classref-item-separator

----

.. _class_BackBufferCopy_property_rect:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **rect** = ``Rect2(-100, -100, 200, 200)`` :ref:`🔗<class_BackBufferCopy_property_rect>`

.. rst-class:: classref-property-setget

- |void| **set_rect**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_rect**\ (\ )

Vùng được **BackBufferCopy** bao phủ. Chỉ được sử dụng nếu :ref:`copy_mode<class_BackBufferCopy_property_copy_mode>` là :ref:`COPY_MODE_RECT<class_BackBufferCopy_constant_COPY_MODE_RECT>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
