:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/noise/doc_classes/Noise.xml.

.. _class_Noise:

Nhiễu
=====

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`FastNoiseLite<class_FastNoiseLite>`

Lớp cơ sở trừu tượng cho các trình tạo nhiễu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này định nghĩa interface để các thư viện tạo nhiễu kế thừa.

Một triển khai :ref:`get_seamless_image()<class_Noise_method_get_seamless_image>` mặc định được cung cấp cho các thư viện không cung cấp nhiễu liền mạch. Hàm này yêu cầu một ảnh lớn hơn từ phương thức :ref:`get_image()<class_Noise_method_get_image>`, đảo vị trí các góc phần tư của ảnh, sau đó sử dụng các dải có chiều rộng bổ sung để hòa trộn lên các đường nối.

Các lớp nhiễu kế thừa có thể tùy chọn ghi đè hàm này để cung cấp một thuật toán tối ưu hơn.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Image<class_Image>`                              | :ref:`get_image<class_Noise_method_get_image>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, in_3d_space\: :ref:`bool<class_bool>` = false, normalize\: :ref:`bool<class_bool>` = true\ ) |const|                                                            |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\] | :ref:`get_image_3d<class_Noise_method_get_image_3d>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, normalize\: :ref:`bool<class_bool>` = true\ ) |const|                                                                      |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                              | :ref:`get_noise_1d<class_Noise_method_get_noise_1d>`\ (\ x\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                                                           |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                              | :ref:`get_noise_2d<class_Noise_method_get_noise_2d>`\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                            |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                              | :ref:`get_noise_2dv<class_Noise_method_get_noise_2dv>`\ (\ v\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                                                                                                                                                                                     |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                              | :ref:`get_noise_3d<class_Noise_method_get_noise_3d>`\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`, z\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                             |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                              | :ref:`get_noise_3dv<class_Noise_method_get_noise_3dv>`\ (\ v\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                                                                                                                     |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Image<class_Image>`                              | :ref:`get_seamless_image<class_Noise_method_get_seamless_image>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, in_3d_space\: :ref:`bool<class_bool>` = false, skirt\: :ref:`float<class_float>` = 0.1, normalize\: :ref:`bool<class_bool>` = true\ ) |const| |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\] | :ref:`get_seamless_image_3d<class_Noise_method_get_seamless_image_3d>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, skirt\: :ref:`float<class_float>` = 0.1, normalize\: :ref:`bool<class_bool>` = true\ ) |const|           |
   +--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Noise_method_get_image:

.. rst-class:: classref-method

:ref:`Image<class_Image>` **get_image**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, in_3d_space\: :ref:`bool<class_bool>` = false, normalize\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Noise_method_get_image>`

Trả về một :ref:`Image<class_Image>` chứa các giá trị nhiễu 2D.

\ **Lưu ý:** Khi ``normalize`` được đặt thành ``false``, triển khai mặc định yêu cầu trình tạo nhiễu trả về các giá trị trong khoảng từ ``-1.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_image_3d:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\] **get_image_3d**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, normalize\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Noise_method_get_image_3d>`

Trả về một :ref:`Array<class_Array>` gồm :ref:`Image<class_Image>`\ s chứa các giá trị nhiễu 3D để sử dụng với :ref:`ImageTexture3D.create()<class_ImageTexture3D_method_create>`.

\ **Lưu ý:** Khi ``normalize`` được đặt thành ``false``, triển khai mặc định yêu cầu trình tạo nhiễu trả về các giá trị trong khoảng từ ``-1.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_noise_1d:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_noise_1d**\ (\ x\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Noise_method_get_noise_1d>`

Trả về giá trị nhiễu 1D tại tọa độ (x) đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_noise_2d:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_noise_2d**\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Noise_method_get_noise_2d>`

Trả về giá trị nhiễu 2D tại vị trí đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_noise_2dv:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_noise_2dv**\ (\ v\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Noise_method_get_noise_2dv>`

Trả về giá trị nhiễu 2D tại vị trí đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_noise_3d:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_noise_3d**\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`, z\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Noise_method_get_noise_3d>`

Trả về giá trị nhiễu 3D tại vị trí đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_noise_3dv:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_noise_3dv**\ (\ v\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Noise_method_get_noise_3dv>`

Trả về giá trị nhiễu 3D tại vị trí đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_seamless_image:

.. rst-class:: classref-method

:ref:`Image<class_Image>` **get_seamless_image**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, in_3d_space\: :ref:`bool<class_bool>` = false, skirt\: :ref:`float<class_float>` = 0.1, normalize\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Noise_method_get_seamless_image>`

Trả về một :ref:`Image<class_Image>` chứa các giá trị nhiễu 2D liền mạch.

\ **Lưu ý:** Khi ``normalize`` được đặt thành ``false``, triển khai mặc định yêu cầu trình tạo nhiễu trả về các giá trị trong khoảng từ ``-1.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_Noise_method_get_seamless_image_3d:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\] **get_seamless_image_3d**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, invert\: :ref:`bool<class_bool>` = false, skirt\: :ref:`float<class_float>` = 0.1, normalize\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Noise_method_get_seamless_image_3d>`

Trả về một :ref:`Array<class_Array>` gồm :ref:`Image<class_Image>`\ s chứa các giá trị nhiễu 3D liền mạch để sử dụng với :ref:`ImageTexture3D.create()<class_ImageTexture3D_method_create>`.

\ **Lưu ý:** Khi ``normalize`` được đặt thành ``false``, triển khai mặc định yêu cầu trình tạo nhiễu trả về các giá trị trong khoảng từ ``-1.0`` đến ``1.0``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
