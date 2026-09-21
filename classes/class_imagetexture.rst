:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ImageTexture.xml.

.. _class_ImageTexture:

ImageTexture
============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`Texture2D<class_Texture2D>` dựa trên một :ref:`Image<class_Image>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một :ref:`Texture2D<class_Texture2D>` dựa trên một :ref:`Image<class_Image>`. Để hiển thị một hình ảnh, cần tạo **ImageTexture** từ hình ảnh đó bằng phương thức :ref:`create_from_image()<class_ImageTexture_method_create_from_image>`:

::

    var image = Image.load_from_file("res://icon.svg")
    var texture = ImageTexture.create_from_image(image)
    $Sprite2D.texture = texture

Bằng cách này, texture có thể được tạo lúc runtime bằng cách tải hình ảnh từ cả bên trong editor lẫn bên ngoài.

\ **Cảnh báo:** Ưu tiên tải các texture đã import bằng :ref:`@GDScript.load()<class_@GDScript_method_load>` thay vì tải động chúng từ filesystem bằng :ref:`Image.load()<class_Image_method_load>`, vì cách này có thể không hoạt động trong các project đã export:

::

    var texture = load("res://icon.svg")
    $Sprite2D.texture = texture

Lý do là hình ảnh trước tiên phải được import dưới dạng :ref:`CompressedTexture2D<class_CompressedTexture2D>` để có thể tải bằng :ref:`@GDScript.load()<class_@GDScript_method_load>`. Nếu bạn vẫn muốn tải một tệp hình ảnh giống như bất kỳ :ref:`Resource<class_Resource>` nào khác, hãy import tệp đó dưới dạng tài nguyên :ref:`Image<class_Image>`, sau đó tải bình thường bằng phương thức :ref:`@GDScript.load()<class_@GDScript_method_load>`.

\ **Lưu ý:** Có thể lấy hình ảnh từ một texture đã import bằng phương thức :ref:`Texture2D.get_image()<class_Texture2D_method_get_image>`, phương thức này trả về một bản sao của hình ảnh:

::

    var texture = load("res://icon.svg")
    var image = texture.get_image()

**ImageTexture** không được thiết kế để thao tác trực tiếp từ giao diện editor và chủ yếu hữu ích cho việc render hình ảnh lên màn hình một cách động thông qua code. Nếu bạn cần tạo hình ảnh theo quy trình (procedurally) từ bên trong editor, hãy cân nhắc lưu và import hình ảnh dưới dạng các tài nguyên texture tùy chỉnh triển khai một :ref:`EditorImportPlugin<class_EditorImportPlugin>` mới.

\ **Lưu ý:** Kích thước texture tối đa là 16384×16384 pixel do các giới hạn của phần cứng đồ họa.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Importing images <../tutorials/assets_pipeline/importing_images>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+-------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | resource_local_to_scene | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------+-------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ImageTexture<class_ImageTexture>` | :ref:`create_from_image<class_ImageTexture_method_create_from_image>`\ (\ image\: :ref:`Image<class_Image>`\ ) |static| |
   +-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | |void|                                  | :ref:`set_image<class_ImageTexture_method_set_image>`\ (\ image\: :ref:`Image<class_Image>`\ )                          |
   +-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | |void|                                  | :ref:`set_size_override<class_ImageTexture_method_set_size_override>`\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ )     |
   +-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | |void|                                  | :ref:`update<class_ImageTexture_method_update>`\ (\ image\: :ref:`Image<class_Image>`\ )                                |
   +-----------------------------------------+-------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ImageTexture_method_create_from_image:

.. rst-class:: classref-method

:ref:`ImageTexture<class_ImageTexture>` **create_from_image**\ (\ image\: :ref:`Image<class_Image>`\ ) |static| :ref:`🔗<class_ImageTexture_method_create_from_image>`

Tạo một **ImageTexture** mới và khởi tạo texture bằng cách cấp phát và thiết lập dữ liệu từ một :ref:`Image<class_Image>`.

.. rst-class:: classref-item-separator

----

.. _class_ImageTexture_method_set_image:

.. rst-class:: classref-method

|void| **set_image**\ (\ image\: :ref:`Image<class_Image>`\ ) :ref:`🔗<class_ImageTexture_method_set_image>`

Thay thế dữ liệu của texture bằng một :ref:`Image<class_Image>` mới. Thao tác này sẽ cấp phát lại bộ nhớ mới cho texture.

Nếu bạn muốn cập nhật hình ảnh nhưng không cần thay đổi các tham số của hình ảnh (định dạng, kích thước), hãy dùng :ref:`update()<class_ImageTexture_method_update>` thay thế để có hiệu năng tốt hơn.

.. rst-class:: classref-item-separator

----

.. _class_ImageTexture_method_set_size_override:

.. rst-class:: classref-method

|void| **set_size_override**\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_ImageTexture_method_set_size_override>`

Thay đổi kích thước texture theo các kích thước đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_ImageTexture_method_update:

.. rst-class:: classref-method

|void| **update**\ (\ image\: :ref:`Image<class_Image>`\ ) :ref:`🔗<class_ImageTexture_method_update>`

Thay thế dữ liệu của texture bằng một :ref:`Image<class_Image>` mới.

\ **Lưu ý:** Texture phải được tạo bằng :ref:`create_from_image()<class_ImageTexture_method_create_from_image>` hoặc được khởi tạo trước bằng phương thức :ref:`set_image()<class_ImageTexture_method_set_image>` thì mới có thể cập nhật. Kích thước hình ảnh, định dạng và cấu hình mipmap của hình ảnh mới phải khớp với cấu hình hình ảnh của texture hiện có.

Hãy dùng phương thức này thay cho :ref:`set_image()<class_ImageTexture_method_set_image>` nếu bạn cần cập nhật texture thường xuyên, vì cách này nhanh hơn so với việc cấp phát thêm bộ nhớ cho một texture mới mỗi lần.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
