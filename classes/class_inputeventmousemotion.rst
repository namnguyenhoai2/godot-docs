:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventMouseMotion.xml.

.. _class_InputEventMouseMotion:

InputEventMouseMotion
=====================

**Kế thừa:** :ref:`InputEventMouse<class_InputEventMouse>` **<** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Biểu thị chuyển động của chuột hoặc bút.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về chuyển động của chuột hoặc bút. Thông tin này bao gồm vị trí tương đối, vị trí tuyệt đối và velocity. Xem :ref:`Node._input()<class_Node_private_method__input>`.

\ **Lưu ý:** Theo mặc định, sự kiện này chỉ được phát tối đa một lần trong mỗi frame được render. Nếu cần báo cáo input chính xác hơn, hãy đặt :ref:`Input.use_accumulated_input<class_Input_property_use_accumulated_input>` thành ``false`` để các sự kiện được phát thường xuyên nhất có thể. Nếu sử dụng InputEventMouseMotion để vẽ đường, hãy cân nhắc sử dụng cả :ref:`Geometry2D.bresenham_line()<class_Geometry2D_method_bresenham_line>` để tránh các khoảng trống dễ nhận thấy trên đường vẽ khi người dùng di chuyển chuột nhanh.

\ **Lưu ý:** Sự kiện này có thể được phát ngay cả khi chuột không di chuyển, bởi hệ điều hành hoặc chính Godot. Nếu thực sự cần biết chuột có di chuyển hay không (ví dụ: để ngăn hiển thị tooltip), bạn nên kiểm tra ``relative.is_zero_approx()`` là ``false``.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

- :doc:`Tọa độ chuột và input <../tutorials/inputs/mouse_and_input_coordinates>`

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`       | :ref:`pen_inverted<class_InputEventMouseMotion_property_pen_inverted>`       | ``false``         |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`     | :ref:`pressure<class_InputEventMouseMotion_property_pressure>`               | ``0.0``           |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`relative<class_InputEventMouseMotion_property_relative>`               | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`screen_relative<class_InputEventMouseMotion_property_screen_relative>` | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`screen_velocity<class_InputEventMouseMotion_property_screen_velocity>` | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`tilt<class_InputEventMouseMotion_property_tilt>`                       | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`velocity<class_InputEventMouseMotion_property_velocity>`               | ``Vector2(0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventMouseMotion_property_pen_inverted:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pen_inverted** = ``false`` :ref:`🔗<class_InputEventMouseMotion_property_pen_inverted>`

.. rst-class:: classref-property-setget

- |void| **set_pen_inverted**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_pen_inverted**\ (\ )

Trả về ``true`` khi sử dụng đầu tẩy của bút stylus.

\ **Lưu ý:** Thuộc tính này được triển khai trên Linux, macOS và Windows.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_pressure:

.. rst-class:: classref-property

:ref:`float<class_float>` **pressure** = ``0.0`` :ref:`🔗<class_InputEventMouseMotion_property_pressure>`

.. rst-class:: classref-property-setget

- |void| **set_pressure**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pressure**\ (\ )

Biểu thị lực người dùng tác động lên bút. Có giá trị từ ``0.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_relative:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **relative** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouseMotion_property_relative>`

.. rst-class:: classref-property-setget

- |void| **set_relative**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_relative**\ (\ )

Vị trí chuột tương đối so với vị trí trước đó (vị trí ở frame trước).

\ **Lưu ý:** Vì **InputEventMouseMotion** có thể chỉ được phát khi chuột di chuyển, không thể phát hiện một cách đáng tin cậy thời điểm chuột dừng di chuyển bằng cách kiểm tra thuộc tính này. Có thể cần một timer ngắn riêng biệt.

\ **Lưu ý:** :ref:`relative<class_InputEventMouseMotion_property_relative>` được tự động scale theo content scale factor, được xác định bởi các thiết lập stretch mode của project. Điều này có nghĩa là độ nhạy chuột sẽ có vẻ khác nhau tùy theo độ phân giải khi sử dụng :ref:`relative<class_InputEventMouseMotion_property_relative>` trong một script xử lý việc ngắm bằng chuột với mouse mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`. Để tránh điều này, hãy sử dụng :ref:`screen_relative<class_InputEventMouseMotion_property_screen_relative>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_screen_relative:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **screen_relative** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouseMotion_property_screen_relative>`

.. rst-class:: classref-property-setget

- |void| **set_screen_relative**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_screen_relative**\ (\ )

Vị trí chuột tương đối chưa scale so với vị trí trước đó trong hệ tọa độ màn hình (vị trí ở frame trước).

\ **Lưu ý:** Vì **InputEventMouseMotion** có thể chỉ được phát khi chuột di chuyển, không thể phát hiện một cách đáng tin cậy thời điểm chuột dừng di chuyển bằng cách kiểm tra thuộc tính này. Có thể cần một timer ngắn riêng biệt.

\ **Lưu ý:** Tọa độ này *không* được scale theo content scale factor hoặc các lệnh gọi :ref:`InputEvent.xformed_by()<class_InputEvent_method_xformed_by>`. Nên ưu tiên thuộc tính này hơn :ref:`relative<class_InputEventMouseMotion_property_relative>` để ngắm bằng chuột khi sử dụng mouse mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`, bất kể stretch mode của project.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_screen_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **screen_velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouseMotion_property_screen_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_screen_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_screen_velocity**\ (\ )

Velocity chưa scale của chuột, tính bằng pixel trên giây trong tọa độ màn hình. Velocity này *không* được scale theo content scale factor hoặc các lệnh gọi :ref:`InputEvent.xformed_by()<class_InputEvent_method_xformed_by>`.

\ **Lưu ý:** Trong mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`, :ref:`screen_velocity<class_InputEventMouseMotion_property_screen_velocity>` trả về ``(0, 0)`` vì con trỏ chuột bị ẩn và khóa. Sử dụng :ref:`screen_relative<class_InputEventMouseMotion_property_screen_relative>` để ngắm bằng chuột khi sử dụng mouse mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_tilt:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **tilt** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouseMotion_property_tilt>`

.. rst-class:: classref-property-setget

- |void| **set_tilt**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_tilt**\ (\ )

Biểu thị các góc nghiêng của bút. Giá trị tọa độ X dương biểu thị bút nghiêng sang phải. Giá trị tọa độ Y dương biểu thị bút nghiêng về phía người dùng. Cả hai trục đều có giá trị từ ``-1.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseMotion_property_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouseMotion_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_velocity**\ (\ )

Velocity của chuột, tính bằng pixel trên giây.

\ **Lưu ý:** :ref:`velocity<class_InputEventMouseMotion_property_velocity>` được tự động scale theo content scale factor, được xác định bởi các thiết lập stretch mode của project. Điều đó có nghĩa là độ nhạy chuột có thể có vẻ khác nhau tùy theo độ phân giải.

\ **Lưu ý:** Trong mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`, :ref:`velocity<class_InputEventMouseMotion_property_velocity>` trả về ``(0, 0)`` vì con trỏ chuột bị ẩn và khóa. Sử dụng :ref:`screen_relative<class_InputEventMouseMotion_property_screen_relative>` để ngắm bằng chuột khi sử dụng mouse mode :ref:`Input.MOUSE_MODE_CAPTURED<class_Input_constant_MOUSE_MODE_CAPTURED>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
