:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InstancePlaceholder.xml.

.. _class_InstancePlaceholder:

InstancePlaceholder
===================

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Placeholder cho :ref:`Node<class_Node>` gốc của một :ref:`PackedScene<class_PackedScene>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bật tùy chọn **Load As Placeholder** cho một scene được instantiate trong editor sẽ khiến scene đó được thay thế bằng một **InstancePlaceholder** khi chạy game; node trong editor sẽ không bị thay thế. Điều này cho phép trì hoãn việc thực sự load scene cho đến khi gọi :ref:`create_instance()<class_InstancePlaceholder_method_create_instance>`. Tùy chọn này hữu ích để tránh load tất cả các scene lớn cùng một lúc bằng cách load có chọn lọc từng phần của chúng.

\ **Lưu ý:** Giống như :ref:`Node<class_Node>`, **InstancePlaceholder** không có transform. Vì vậy, mọi node con sẽ được định vị tương đối so với origin của :ref:`Viewport<class_Viewport>`, thay vì node cha như hiển thị trong editor. Khi thay placeholder bằng một scene có transform, các node con sẽ lại được transform tương đối so với node cha.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`             | :ref:`create_instance<class_InstancePlaceholder_method_create_instance>`\ (\ replace\: :ref:`bool<class_bool>` = false, custom_scene\: :ref:`PackedScene<class_PackedScene>` = null\ ) |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`         | :ref:`get_instance_path<class_InstancePlaceholder_method_get_instance_path>`\ (\ ) |const|                                                                                             |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`get_stored_values<class_InstancePlaceholder_method_get_stored_values>`\ (\ with_order\: :ref:`bool<class_bool>` = false\ )                                                       |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_InstancePlaceholder_method_create_instance:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **create_instance**\ (\ replace\: :ref:`bool<class_bool>` = false, custom_scene\: :ref:`PackedScene<class_PackedScene>` = null\ ) :ref:`🔗<class_InstancePlaceholder_method_create_instance>`

Gọi method này để thực sự load node. Node được tạo sẽ được đặt làm sibling *ở phía trên* **InstancePlaceholder** trong scene tree. Tham chiếu đến :ref:`Node<class_Node>` cũng được trả về để thuận tiện.

\ **Lưu ý:** :ref:`create_instance()<class_InstancePlaceholder_method_create_instance>` không thread-safe. Hãy sử dụng :ref:`Object.call_deferred()<class_Object_method_call_deferred>` nếu gọi từ một thread.

.. rst-class:: classref-item-separator

----

.. _class_InstancePlaceholder_method_get_instance_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_instance_path**\ (\ ) |const| :ref:`🔗<class_InstancePlaceholder_method_get_instance_path>`

Lấy đường dẫn đến tệp resource :ref:`PackedScene<class_PackedScene>` được load mặc định khi gọi :ref:`create_instance()<class_InstancePlaceholder_method_create_instance>`. Không thread-safe. Hãy sử dụng :ref:`Object.call_deferred()<class_Object_method_call_deferred>` nếu gọi từ một thread.

.. rst-class:: classref-item-separator

----

.. _class_InstancePlaceholder_method_get_stored_values:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_stored_values**\ (\ with_order\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_InstancePlaceholder_method_get_stored_values>`

Trả về danh sách các property sẽ được áp dụng cho node khi :ref:`create_instance()<class_InstancePlaceholder_method_create_instance>` được gọi.

Nếu ``with_order`` là ``true``, một key có tên ``.order`` (lưu ý dấu chấm ở đầu) sẽ được thêm vào dictionary. Key ``.order`` này là một :ref:`Array<class_Array>` gồm các tên property của :ref:`String<class_String>`, xác định thứ tự áp dụng các property (index 0 là property đầu tiên).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
