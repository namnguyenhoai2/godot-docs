:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ImageTextureLayered.xml.

.. _class_ImageTextureLayered:

ImageTextureLayered
===================

**Kế thừa:** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`Cubemap<class_Cubemap>`, :ref:`CubemapArray<class_CubemapArray>`, :ref:`Texture2DArray<class_Texture2DArray>`

Lớp cơ sở cho các loại texture chứa dữ liệu của nhiều :ref:`ImageTexture<class_ImageTexture>`\ s. Mỗi image có cùng kích thước và định dạng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho :ref:`Texture2DArray<class_Texture2DArray>`, :ref:`Cubemap<class_Cubemap>` và :ref:`CubemapArray<class_CubemapArray>`. Không thể sử dụng trực tiếp, nhưng chứa tất cả các hàm cần thiết để truy cập những loại resource dẫn xuất. Xem thêm :ref:`Texture3D<class_Texture3D>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`create_from_images<class_ImageTextureLayered_method_create_from_images>`\ (\ images\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ ) |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`update_layer<class_ImageTextureLayered_method_update_layer>`\ (\ image\: :ref:`Image<class_Image>`, layer\: :ref:`int<class_int>`\ )            |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ImageTextureLayered_method_create_from_images:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_from_images**\ (\ images\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ ) :ref:`🔗<class_ImageTextureLayered_method_create_from_images>`

Tạo một **ImageTextureLayered** từ một mảng các :ref:`Image<class_Image>`\ s. Xem :ref:`Image.create()<class_Image_method_create>` để biết định dạng dữ liệu dự kiến. Image đầu tiên quyết định chiều rộng, chiều cao, định dạng image và thiết lập mipmapping. Các image còn lại *phải* có cùng chiều rộng, chiều cao, định dạng image và thiết lập mipmapping.

Mỗi :ref:`Image<class_Image>` đại diện cho một ``layer``.

::

    # Điền một mảng Images bằng các màu khác nhau.
    var images = []
    const LAYERS = 6
    for i in LAYERS:
        var image = Image.create_empty(128, 128, false, Image.FORMAT_RGB8)
        if i % 3 == 0:
            image.fill(Color.RED)
        elif i % 3 == 1:
            image.fill(Color.GREEN)
        else:
            image.fill(Color.BLUE)
        images.push_back(image)

    # Tạo và lưu một mảng texture 2D. Mảng images phải có ít nhất 1 Image.
    var texture_2d_array = Texture2DArray.new()
    texture_2d_array.create_from_images(images)
    ResourceSaver.save(texture_2d_array, "res://texture_2d_array.res", ResourceSaver.FLAG_COMPRESS)

    # Tạo và lưu một cubemap. Mảng images phải có chính xác 6 Image.
    # Các image của cubemap được chỉ định theo thứ tự này: X+, X-, Y+, Y-, Z+, Z-
    # (trong hệ tọa độ của Godot, vì vậy Y+ là "lên" và Z- là "hướng về phía trước").
    var cubemap = Cubemap.new()
    cubemap.create_from_images(images)
    ResourceSaver.save(cubemap, "res://cubemap.res", ResourceSaver.FLAG_COMPRESS)

    # Tạo và lưu một mảng cubemap. Mảng images phải có số lượng Image là bội số của 6.
    # Các image của mỗi cubemap được chỉ định theo thứ tự này: X+, X-, Y+, Y-, Z+, Z-
    # (trong hệ tọa độ của Godot, vì vậy Y+ là "lên" và Z- là "hướng về phía trước").
    var cubemap_array = CubemapArray.new()
    cubemap_array.create_from_images(images)
    ResourceSaver.save(cubemap_array, "res://cubemap_array.res", ResourceSaver.FLAG_COMPRESS)

.. rst-class:: classref-item-separator

----

.. _class_ImageTextureLayered_method_update_layer:

.. rst-class:: classref-method

|void| **update_layer**\ (\ image\: :ref:`Image<class_Image>`, layer\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ImageTextureLayered_method_update_layer>`

Thay thế dữ liệu :ref:`Image<class_Image>` hiện có tại ``layer`` đã cho bằng image mới này.

:ref:`Image<class_Image>` đã cho phải có cùng chiều rộng, chiều cao, định dạng image và cờ mipmapping như các image được tham chiếu còn lại.

Nếu định dạng image không được hỗ trợ, image sẽ được giải nén và chuyển đổi sang một :ref:`Format<enum_Image_Format>` tương tự và được hỗ trợ.

Việc cập nhật diễn ra ngay lập tức: nó được đồng bộ với quá trình vẽ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
