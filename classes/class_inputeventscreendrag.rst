:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventScreenDrag.xml.

.. _class_InputEventScreenDrag:

InputEventScreenDrag
====================

**Kế thừa:** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một sự kiện kéo trên màn hình.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các sự kiện kéo trên màn hình. Xem :ref:`Node._input()<class_Node_private_method__input>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`         | :ref:`index<class_InputEventScreenDrag_property_index>`                     | ``0``             |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`pen_inverted<class_InputEventScreenDrag_property_pen_inverted>`       | ``false``         |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`position<class_InputEventScreenDrag_property_position>`               | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`pressure<class_InputEventScreenDrag_property_pressure>`               | ``0.0``           |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`relative<class_InputEventScreenDrag_property_relative>`               | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`screen_relative<class_InputEventScreenDrag_property_screen_relative>` | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`screen_velocity<class_InputEventScreenDrag_property_screen_velocity>` | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`tilt<class_InputEventScreenDrag_property_tilt>`                       | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`velocity<class_InputEventScreenDrag_property_velocity>`               | ``Vector2(0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventScreenDrag_property_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **index** = ``0`` :ref:`🔗<class_InputEventScreenDrag_property_index>`

.. rst-class:: classref-property-setget

- |void| **set_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_index**\ (\ )

Chỉ mục của sự kiện kéo trong trường hợp sự kiện kéo nhiều điểm.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_pen_inverted:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pen_inverted** = ``false`` :ref:`🔗<class_InputEventScreenDrag_property_pen_inverted>`

.. rst-class:: classref-property-setget

- |void| **set_pen_inverted**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_pen_inverted**\ (\ )

Trả về ``true`` khi sử dụng đầu tẩy của bút stylus.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Vị trí kéo trong viewport mà node đang nằm trong đó, sử dụng hệ tọa độ của viewport này.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_pressure:

.. rst-class:: classref-property

:ref:`float<class_float>` **pressure** = ``0.0`` :ref:`🔗<class_InputEventScreenDrag_property_pressure>`

.. rst-class:: classref-property-setget

- |void| **set_pressure**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pressure**\ (\ )

Đại diện cho lực người dùng tác động lên bút. Nằm trong khoảng từ ``0.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_relative:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **relative** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_relative>`

.. rst-class:: classref-property-setget

- |void| **set_relative**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_relative**\ (\ )

Vị trí kéo tương đối so với vị trí trước đó (vị trí ở frame trước).

\ **Lưu ý:** :ref:`relative<class_InputEventScreenDrag_property_relative>` được tự động scale theo hệ số scale nội dung, được xác định bởi các thiết lập stretch mode của project. Điều này có nghĩa là độ nhạy cảm ứng sẽ khác nhau tùy theo độ phân giải khi sử dụng :ref:`relative<class_InputEventScreenDrag_property_relative>` trong một script xử lý việc ngắm bằng cảm ứng. Để tránh điều này, hãy sử dụng :ref:`screen_relative<class_InputEventScreenDrag_property_screen_relative>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_screen_relative:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **screen_relative** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_screen_relative>`

.. rst-class:: classref-property-setget

- |void| **set_screen_relative**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_screen_relative**\ (\ )

Vị trí kéo tương đối chưa scale so với vị trí trước đó trong tọa độ màn hình (vị trí ở frame trước). Vị trí này *không* được scale theo hệ số scale nội dung hoặc các lần gọi đến :ref:`InputEvent.xformed_by()<class_InputEvent_method_xformed_by>`. Nên ưu tiên sử dụng thuộc tính này hơn :ref:`relative<class_InputEventScreenDrag_property_relative>` cho việc ngắm bằng cảm ứng, bất kể stretch mode của project.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_screen_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **screen_velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_screen_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_screen_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_screen_velocity**\ (\ )

Vận tốc kéo chưa scale tính bằng pixel mỗi giây trong tọa độ màn hình. Vận tốc này *không* được scale theo hệ số scale nội dung hoặc các lần gọi đến :ref:`InputEvent.xformed_by()<class_InputEvent_method_xformed_by>`. Nên ưu tiên sử dụng thuộc tính này hơn :ref:`velocity<class_InputEventScreenDrag_property_velocity>` cho việc ngắm bằng cảm ứng, bất kể stretch mode của project.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_tilt:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **tilt** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_tilt>`

.. rst-class:: classref-property-setget

- |void| **set_tilt**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_tilt**\ (\ )

Đại diện cho các góc nghiêng của bút. Giá trị tọa độ X dương cho biết bút nghiêng sang phải. Giá trị tọa độ Y dương cho biết bút nghiêng về phía người dùng. Với cả hai trục, giá trị nằm trong khoảng từ ``-1.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_InputEventScreenDrag_property_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventScreenDrag_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_velocity**\ (\ )

Vận tốc kéo.

\ **Lưu ý:** :ref:`velocity<class_InputEventScreenDrag_property_velocity>` được tự động scale theo hệ số scale nội dung, được xác định bởi các thiết lập stretch mode của project. Điều này có nghĩa là độ nhạy cảm ứng sẽ khác nhau tùy theo độ phân giải khi sử dụng :ref:`velocity<class_InputEventScreenDrag_property_velocity>` trong một script xử lý việc ngắm bằng cảm ứng. Để tránh điều này, hãy sử dụng :ref:`screen_velocity<class_InputEventScreenDrag_property_screen_velocity>` thay thế.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
