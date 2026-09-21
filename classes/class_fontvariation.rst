:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FontVariation.xml.

.. _class_FontVariation:

FontVariation
=============

**Kế thừa:** :ref:`Font<class_Font>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một biến thể của font với các thiết lập bổ sung.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp các biến thể OpenType, kiểu đậm / nghiêng mô phỏng và các thiết lập font bổ sung như các tính năng OpenType và khoảng cách bổ sung.

Để sử dụng biến thể font đậm mô phỏng:


.. tabs::

 .. code-tab:: gdscript

    var fv = FontVariation.new()
    fv.base_font = load("res://BarlowCondensed-Regular.ttf")
    fv.variation_embolden = 1.2
    $Label.add_theme_font_override("font", fv)
    $Label.add_theme_font_size_override("font_size", 64)

 .. code-tab:: csharp

    var fv = new FontVariation();
    fv.SetBaseFont(ResourceLoader.Load<FontFile>("res://BarlowCondensed-Regular.ttf"));
    fv.SetVariationEmbolden(1.2);
    GetNode("Label").AddThemeFontOverride("font", fv);
    GetNode("Label").AddThemeFontSizeOverride("font_size", 64);



Để đặt tọa độ của nhiều trục biến thể:

::

    var fv = FontVariation.new();
    var ts = TextServerManager.get_primary_interface()
    fv.base_font = load("res://BarlowCondensed-Regular.ttf")
    fv.variation_opentype = { ts.name_to_tag("wght"): 900, ts.name_to_tag("custom_hght"): 900 }

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Font<class_Font>`                         | :ref:`base_font<class_FontVariation_property_base_font>`                         |                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`                       | :ref:`baseline_offset<class_FontVariation_property_baseline_offset>`             | ``0.0``                           |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Dictionary<class_Dictionary>`             | :ref:`opentype_features<class_FontVariation_property_opentype_features>`         | ``{}``                            |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`palette_custom_colors<class_FontVariation_property_palette_custom_colors>` | ``PackedColorArray()``            |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`palette_index<class_FontVariation_property_palette_index>`                 | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`spacing_bottom<class_FontVariation_property_spacing_bottom>`               | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`spacing_glyph<class_FontVariation_property_spacing_glyph>`                 | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`spacing_space<class_FontVariation_property_spacing_space>`                 | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`spacing_top<class_FontVariation_property_spacing_top>`                     | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`                       | :ref:`variation_embolden<class_FontVariation_property_variation_embolden>`       | ``0.0``                           |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                           | :ref:`variation_face_index<class_FontVariation_property_variation_face_index>`   | ``0``                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Dictionary<class_Dictionary>`             | :ref:`variation_opentype<class_FontVariation_property_variation_opentype>`       | ``{}``                            |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>`           | :ref:`variation_transform<class_FontVariation_property_variation_transform>`     | ``Transform2D(1, 0, 0, 1, 0, 0)`` |
   +-------------------------------------------------+----------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`set_spacing<class_FontVariation_method_set_spacing>`\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) |
   +--------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FontVariation_property_base_font:

.. rst-class:: classref-property

:ref:`Font<class_Font>` **base_font** :ref:`🔗<class_FontVariation_property_base_font>`

.. rst-class:: classref-property-setget

- |void| **set_base_font**\ (\ value\: :ref:`Font<class_Font>`\ ) - :ref:`Font<class_Font>` **get_base_font**\ (\ )

Font cơ sở được dùng để tạo biến thể. Nếu chưa được đặt, font :ref:`Theme<class_Theme>` mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_baseline_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **baseline_offset** = ``0.0`` :ref:`🔗<class_FontVariation_property_baseline_offset>`

.. rst-class:: classref-property-setget

- |void| **set_baseline_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_baseline_offset**\ (\ )

Độ lệch baseline bổ sung (theo tỷ lệ chiều cao font).

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_opentype_features:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **opentype_features** = ``{}`` :ref:`🔗<class_FontVariation_property_opentype_features>`

.. rst-class:: classref-property-setget

- |void| **set_opentype_features**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_opentype_features**\ (\ )

Một tập các thẻ tính năng OpenType. Thông tin thêm: `OpenType feature tags <https://docs.microsoft.com/en-us/typography/opentype/spec/featuretags>`__.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_palette_custom_colors:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **palette_custom_colors** = ``PackedColorArray()`` :ref:`🔗<class_FontVariation_property_palette_custom_colors>`

.. rst-class:: classref-property-setget

- |void| **set_palette_custom_colors**\ (\ value\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) - :ref:`PackedColorArray<class_PackedColorArray>` **get_palette_custom_colors**\ (\ )

Một mảng các màu dùng để ghi đè bảng màu được định nghĩa sẵn. Sử dụng ``Color(0, 0, 0, 0)`` để giữ lại màu của bảng màu được định nghĩa sẵn tại vị trí cụ thể.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_palette_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **palette_index** = ``0`` :ref:`🔗<class_FontVariation_property_palette_index>`

.. rst-class:: classref-property-setget

- |void| **set_palette_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_palette_index**\ (\ )

Một chỉ mục bảng màu.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_spacing_bottom:

.. rst-class:: classref-property

:ref:`int<class_int>` **spacing_bottom** = ``0`` :ref:`🔗<class_FontVariation_property_spacing_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_spacing**\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spacing**\ (\ )

Khoảng cách bổ sung ở phía dưới dòng, tính bằng pixel.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_spacing_glyph:

.. rst-class:: classref-property

:ref:`int<class_int>` **spacing_glyph** = ``0`` :ref:`🔗<class_FontVariation_property_spacing_glyph>`

.. rst-class:: classref-property-setget

- |void| **set_spacing**\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spacing**\ (\ )

Khoảng cách bổ sung giữa các glyph đồ họa.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_spacing_space:

.. rst-class:: classref-property

:ref:`int<class_int>` **spacing_space** = ``0`` :ref:`🔗<class_FontVariation_property_spacing_space>`

.. rst-class:: classref-property-setget

- |void| **set_spacing**\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spacing**\ (\ )

Độ rộng bổ sung của các glyph khoảng trắng.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_spacing_top:

.. rst-class:: classref-property

:ref:`int<class_int>` **spacing_top** = ``0`` :ref:`🔗<class_FontVariation_property_spacing_top>`

.. rst-class:: classref-property-setget

- |void| **set_spacing**\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_spacing**\ (\ )

Khoảng cách bổ sung ở phía trên dòng, tính bằng pixel.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_variation_embolden:

.. rst-class:: classref-property

:ref:`float<class_float>` **variation_embolden** = ``0.0`` :ref:`🔗<class_FontVariation_property_variation_embolden>`

.. rst-class:: classref-property-setget

- |void| **set_variation_embolden**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_variation_embolden**\ (\ )

Nếu khác không, thuộc tính này sẽ làm đậm đường viền của font. Các giá trị âm làm giảm độ dày đường viền.

\ **Lưu ý:** Font được làm đậm có thể có các đường viền tự giao nhau, khiến font MSDF và :ref:`TextMesh<class_TextMesh>` không hoạt động chính xác.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_variation_face_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **variation_face_index** = ``0`` :ref:`🔗<class_FontVariation_property_variation_face_index>`

.. rst-class:: classref-property-setget

- |void| **set_variation_face_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_variation_face_index**\ (\ )

Chỉ mục face đang hoạt động trong tệp tập hợp TrueType / OpenType.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_variation_opentype:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **variation_opentype** = ``{}`` :ref:`🔗<class_FontVariation_property_variation_opentype>`

.. rst-class:: classref-property-setget

- |void| **set_variation_opentype**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_variation_opentype**\ (\ )

Tọa độ biến thể OpenType của font. Thông tin thêm: `OpenType variation tags <https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg>`__.

\ **Lưu ý:** :ref:`Dictionary<class_Dictionary>` này sử dụng các thẻ OpenType làm khóa. Các trục biến thể có thể được xác định bằng cả thẻ (:ref:`int<class_int>`, ví dụ ``0x77678674``) và tên (:ref:`String<class_String>`, ví dụ ``wght``). Một số trục có thể được truy cập bằng nhiều tên. Ví dụ, ``wght`` tham chiếu đến cùng một trục với ``weight``. Ngược lại, các thẻ là duy nhất. Để chuyển đổi giữa tên và thẻ, hãy sử dụng :ref:`TextServer.name_to_tag()<class_TextServer_method_name_to_tag>` và :ref:`TextServer.tag_to_name()<class_TextServer_method_tag_to_name>`.

\ **Lưu ý:** Để lấy các trục biến thể có sẵn của một font, hãy sử dụng :ref:`Font.get_supported_variation_list()<class_Font_method_get_supported_variation_list>`.

.. rst-class:: classref-item-separator

----

.. _class_FontVariation_property_variation_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **variation_transform** = ``Transform2D(1, 0, 0, 1, 0, 0)`` :ref:`🔗<class_FontVariation_property_variation_transform>`

.. rst-class:: classref-property-setget

- |void| **set_variation_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_variation_transform**\ (\ )

Biến đổi 2D được áp dụng cho đường viền font, có thể được sử dụng để làm nghiêng, lật và xoay glyph.

Ví dụ, để mô phỏng kiểu chữ italic bằng cách làm nghiêng, hãy áp dụng biến đổi sau ``Transform2D(1.0, slant, 0.0, 1.0, 0.0, 0.0)``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_FontVariation_method_set_spacing:

.. rst-class:: classref-method

|void| **set_spacing**\ (\ spacing\: :ref:`SpacingType<enum_TextServer_SpacingType>`, value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_FontVariation_method_set_spacing>`

Đặt khoảng cách cho ``spacing`` thành ``value`` pixel (không phụ thuộc vào cỡ font).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
