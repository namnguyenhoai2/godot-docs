:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorResourceTooltipPlugin.xml.

.. _class_EditorResourceTooltipPlugin:

EditorResourceTooltipPlugin
===========================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một plugin cung cấp tooltip nâng cao cho loại resource mà nó xử lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các resource tooltip plugin được :ref:`FileSystemDock<class_FileSystemDock>` sử dụng để tạo tooltip tùy chỉnh cho các resource cụ thể. Ví dụ: tooltip cho một :ref:`Texture2D<class_Texture2D>` hiển thị bản xem trước lớn hơn và kích thước của texture.

Một plugin trước tiên phải được đăng ký với :ref:`FileSystemDock.add_resource_tooltip_plugin()<class_FileSystemDock_method_add_resource_tooltip_plugin>`. Khi người dùng di chuột qua một resource trong filesystem dock được plugin xử lý, :ref:`_make_tooltip_for_path()<class_EditorResourceTooltipPlugin_private_method__make_tooltip_for_path>` sẽ được gọi để tạo tooltip. Nó hoạt động tương tự như :ref:`Control._make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`_handles<class_EditorResourceTooltipPlugin_private_method__handles>`\ (\ type\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                                                                   |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>` | :ref:`_make_tooltip_for_path<class_EditorResourceTooltipPlugin_private_method__make_tooltip_for_path>`\ (\ path\: :ref:`String<class_String>`, metadata\: :ref:`Dictionary<class_Dictionary>`, base\: :ref:`Control<class_Control>`\ ) |virtual| |const| |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`request_thumbnail<class_EditorResourceTooltipPlugin_method_request_thumbnail>`\ (\ path\: :ref:`String<class_String>`, control\: :ref:`TextureRect<class_TextureRect>`\ ) |const|                                                                  |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorResourceTooltipPlugin_private_method__handles:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_handles**\ (\ type\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorResourceTooltipPlugin_private_method__handles>`

Trả về ``true`` nếu plugin sẽ xử lý :ref:`Resource<class_Resource>` đã cho ``type``.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourceTooltipPlugin_private_method__make_tooltip_for_path:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **_make_tooltip_for_path**\ (\ path\: :ref:`String<class_String>`, metadata\: :ref:`Dictionary<class_Dictionary>`, base\: :ref:`Control<class_Control>`\ ) |virtual| |const| :ref:`🔗<class_EditorResourceTooltipPlugin_private_method__make_tooltip_for_path>`

Tạo và trả về một tooltip sẽ được hiển thị khi người dùng di chuột qua một resource nằm dưới ``path`` đã cho trong filesystem dock.

Từ điển ``metadata`` được preview generator cung cấp (xem :ref:`EditorResourcePreviewGenerator._generate()<class_EditorResourcePreviewGenerator_private_method__generate>`).

\ ``base`` là tooltip mặc định cơ sở, một :ref:`VBoxContainer<class_VBoxContainer>` có các nhãn tên tệp, loại và kích thước. Nếu một plugin khác đã xử lý cùng loại tệp, ``base`` sẽ là kết quả từ plugin trước đó. Để đạt kết quả tốt nhất, hãy đảm bảo tooltip cơ sở là một phần của :ref:`Control<class_Control>` được trả về.

\ **Lưu ý:** Không nên sử dụng :ref:`ResourceLoader.load()<class_ResourceLoader_method_load>`, đặc biệt với các resource nặng như model hoặc texture, vì việc này sẽ khiến editor không phản hồi khi tạo tooltip. Bạn có thể sử dụng :ref:`request_thumbnail()<class_EditorResourceTooltipPlugin_method_request_thumbnail>` nếu muốn hiển thị bản xem trước trong tooltip.

\ **Lưu ý:** Nếu bạn quyết định loại bỏ ``base``, hãy đảm bảo gọi :ref:`Node.queue_free()<class_Node_method_queue_free>`, vì nó không được tự động giải phóng.

::

    func _make_tooltip_for_path(path, metadata, base):
        var t_rect = TextureRect.new()
        request_thumbnail(path, t_rect)
        base.add_child(t_rect) # TextureRect sẽ xuất hiện ở cuối tooltip.
        return base

.. rst-class:: classref-item-separator

----

.. _class_EditorResourceTooltipPlugin_method_request_thumbnail:

.. rst-class:: classref-method

|void| **request_thumbnail**\ (\ path\: :ref:`String<class_String>`, control\: :ref:`TextureRect<class_TextureRect>`\ ) |const| :ref:`🔗<class_EditorResourceTooltipPlugin_method_request_thumbnail>`

Yêu cầu một thumbnail cho :ref:`TextureRect<class_TextureRect>` đã cho. Thumbnail được :ref:`EditorResourcePreview<class_EditorResourcePreview>` tạo không đồng bộ và tự động được thiết lập khi sẵn sàng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
