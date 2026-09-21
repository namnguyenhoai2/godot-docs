:github_url: hide

.. meta::
	:keywords: sound

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioListener2D.xml.

.. _class_AudioListener2D:

AudioListener2D
===============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Ghi đè vị trí mà âm thanh được nghe từ đó.

.. rst-class:: classref-introduction-group

Mô tả
-----

Sau khi được thêm vào scene tree và bật bằng :ref:`make_current()<class_AudioListener2D_method_make_current>`, node này sẽ ghi đè vị trí mà âm thanh được nghe từ đó. Chỉ một **AudioListener2D** có thể là current. Sử dụng :ref:`make_current()<class_AudioListener2D_method_make_current>` sẽ vô hiệu hóa **AudioListener2D** trước đó.

Nếu không có **AudioListener2D** đang active trong :ref:`Viewport<class_Viewport>` hiện tại, trung tâm màn hình sẽ được sử dụng làm điểm nghe cho âm thanh. **AudioListener2D** cần nằm bên trong :ref:`SceneTree<class_SceneTree>` để hoạt động.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------+
   | |void|                  | :ref:`clear_current<class_AudioListener2D_method_clear_current>`\ (\ )   |
   +-------------------------+--------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_current<class_AudioListener2D_method_is_current>`\ (\ ) |const| |
   +-------------------------+--------------------------------------------------------------------------+
   | |void|                  | :ref:`make_current<class_AudioListener2D_method_make_current>`\ (\ )     |
   +-------------------------+--------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_AudioListener2D_method_clear_current:

.. rst-class:: classref-method

|void| **clear_current**\ (\ ) :ref:`🔗<class_AudioListener2D_method_clear_current>`

Vô hiệu hóa **AudioListener2D**. Nếu nó chưa được đặt làm current, phương thức này sẽ không có tác dụng.

.. rst-class:: classref-item-separator

----

.. _class_AudioListener2D_method_is_current:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_current**\ (\ ) |const| :ref:`🔗<class_AudioListener2D_method_is_current>`

Trả về ``true`` nếu **AudioListener2D** này hiện đang active.

.. rst-class:: classref-item-separator

----

.. _class_AudioListener2D_method_make_current:

.. rst-class:: classref-method

|void| **make_current**\ (\ ) :ref:`🔗<class_AudioListener2D_method_make_current>`

Kích hoạt **AudioListener2D**, đặt nó làm điểm nghe cho âm thanh. Nếu đã có một **AudioListener2D** khác đang active, node đó sẽ bị vô hiệu hóa.

Phương thức này sẽ không có tác dụng nếu **AudioListener2D** chưa được thêm vào :ref:`SceneTree<class_SceneTree>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
