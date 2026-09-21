:github_url: hide

.. meta::
	:keywords: stain

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Decal.xml.

.. _class_Decal:

Decal
=====

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node chiếu một texture lên :ref:`MeshInstance3D<class_MeshInstance3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Decal**\ s được dùng để chiếu một texture lên :ref:`Mesh<class_Mesh>` trong scene. Sử dụng Decal để thêm chi tiết cho scene mà không ảnh hưởng đến :ref:`Mesh<class_Mesh>` bên dưới. Chúng thường được dùng để thêm dấu hiệu phong hóa cho tòa nhà, thêm bụi bẩn hoặc bùn lên mặt đất, hoặc tạo sự đa dạng cho các prop. Decal có thể được di chuyển bất cứ lúc nào, nên phù hợp cho những thứ như bóng dạng đốm hoặc chấm ngắm laser.

Chúng được tạo từ một :ref:`AABB<class_AABB>` và một nhóm :ref:`Texture2D<class_Texture2D>`\ s chỉ định :ref:`Color<class_Color>`, normal, ORM (ambient occlusion, roughness, metallic) và emission. Decal được chiếu trong phạm vi :ref:`AABB<class_AABB>` của chúng, vì vậy việc thay đổi hướng của Decal sẽ ảnh hưởng đến hướng mà chúng được chiếu. Theo mặc định, Decal được chiếu xuống dưới (tức là từ Y dương đến Y âm).

Các :ref:`Texture2D<class_Texture2D>`\ s liên kết với Decal được tự động lưu trong một texture atlas dùng để vẽ decal, nhờ đó tất cả decal có thể được vẽ cùng lúc. Godot sử dụng clustered decal, nghĩa là chúng được lưu trong cluster data và được vẽ khi mesh được vẽ; chúng không được vẽ như một hiệu ứng hậu kỳ sau đó.

\ **Lưu ý:** Decal không thể ảnh hưởng đến độ trong suốt của material bên dưới, bất kể chế độ trong suốt của material đó là gì (alpha blend, alpha scissor, alpha hash, opaque pre-pass). Điều này có nghĩa là các vùng bán trong suốt hoặc trong suốt của material vẫn sẽ bán trong suốt hoặc trong suốt ngay cả khi áp dụng một decal opaque lên chúng.

\ **Lưu ý:** Decal chỉ được hỗ trợ trong các phương thức render Forward+ và Mobile, không được hỗ trợ trong Compatibility. Khi sử dụng phương thức render Mobile, chỉ có thể hiển thị 8 decal trên mỗi mesh resource. Nếu cố hiển thị nhiều hơn 8 decal trên một mesh resource, các decal sẽ liên tục nhấp nháy khi camera di chuyển.

\ **Lưu ý:** Khi sử dụng phương thức render Mobile, decal chỉ ảnh hưởng chính xác đến các mesh có visibility AABB giao với AABB của decal. Nếu sử dụng shader để biến dạng mesh khiến nó vượt ra ngoài AABB, phải tăng :ref:`GeometryInstance3D.extra_cull_margin<class_GeometryInstance3D_property_extra_cull_margin>` trên mesh. Nếu không, decal có thể không hiển thị trên mesh.

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`albedo_mix<class_Decal_property_albedo_mix>`                       | ``1.0``               |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`             | :ref:`cull_mask<class_Decal_property_cull_mask>`                         | ``1048575``           |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`distance_fade_begin<class_Decal_property_distance_fade_begin>`     | ``40.0``              |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`           | :ref:`distance_fade_enabled<class_Decal_property_distance_fade_enabled>` | ``false``             |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`distance_fade_length<class_Decal_property_distance_fade_length>`   | ``10.0``              |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`emission_energy<class_Decal_property_emission_energy>`             | ``1.0``               |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`lower_fade<class_Decal_property_lower_fade>`                       | ``0.3``               |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`         | :ref:`modulate<class_Decal_property_modulate>`                           | ``Color(1, 1, 1, 1)`` |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`normal_fade<class_Decal_property_normal_fade>`                     | ``0.0``               |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector3<class_Vector3>`     | :ref:`size<class_Decal_property_size>`                                   | ``Vector3(2, 2, 2)``  |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture_albedo<class_Decal_property_texture_albedo>`               |                       |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture_emission<class_Decal_property_texture_emission>`           |                       |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture_normal<class_Decal_property_texture_normal>`               |                       |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture_orm<class_Decal_property_texture_orm>`                     |                       |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`upper_fade<class_Decal_property_upper_fade>`                       | ``0.3``               |
   +-----------------------------------+--------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`get_texture<class_Decal_method_get_texture>`\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const|                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                            | :ref:`set_texture<class_Decal_method_set_texture>`\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_Decal_DecalTexture:

.. rst-class:: classref-enumeration

enum **DecalTexture**: :ref:`🔗<enum_Decal_DecalTexture>`

.. _class_Decal_constant_TEXTURE_ALBEDO:

.. rst-class:: classref-enumeration-constant

:ref:`DecalTexture<enum_Decal_DecalTexture>` **TEXTURE_ALBEDO** = ``0``

:ref:`Texture2D<class_Texture2D>` tương ứng với :ref:`texture_albedo<class_Decal_property_texture_albedo>`.

.. _class_Decal_constant_TEXTURE_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`DecalTexture<enum_Decal_DecalTexture>` **TEXTURE_NORMAL** = ``1``

:ref:`Texture2D<class_Texture2D>` tương ứng với :ref:`texture_normal<class_Decal_property_texture_normal>`.

.. _class_Decal_constant_TEXTURE_ORM:

.. rst-class:: classref-enumeration-constant

:ref:`DecalTexture<enum_Decal_DecalTexture>` **TEXTURE_ORM** = ``2``

:ref:`Texture2D<class_Texture2D>` tương ứng với :ref:`texture_orm<class_Decal_property_texture_orm>`.

.. _class_Decal_constant_TEXTURE_EMISSION:

.. rst-class:: classref-enumeration-constant

:ref:`DecalTexture<enum_Decal_DecalTexture>` **TEXTURE_EMISSION** = ``3``

:ref:`Texture2D<class_Texture2D>` tương ứng với :ref:`texture_emission<class_Decal_property_texture_emission>`.

.. _class_Decal_constant_TEXTURE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`DecalTexture<enum_Decal_DecalTexture>` **TEXTURE_MAX** = ``4``

Kích thước tối đa của enum :ref:`DecalTexture<enum_Decal_DecalTexture>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_Decal_property_albedo_mix:

.. rst-class:: classref-property

:ref:`float<class_float>` **albedo_mix** = ``1.0`` :ref:`🔗<class_Decal_property_albedo_mix>`

.. rst-class:: classref-property-setget

- |void| **set_albedo_mix**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_albedo_mix**\ (\ )

Trộn :ref:`Color<class_Color>` albedo của decal với :ref:`Color<class_Color>` albedo của mesh bên dưới. Có thể đặt thành ``0.0`` để tạo một decal chỉ ảnh hưởng đến normal hoặc ORM. Trong trường hợp này, texture albedo vẫn là bắt buộc vì kênh alpha của nó sẽ xác định vị trí normal và ORM bị ghi đè. Xem thêm :ref:`modulate<class_Decal_property_modulate>`.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **cull_mask** = ``1048575`` :ref:`🔗<class_Decal_property_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_cull_mask**\ (\ )

Chỉ định :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>` nào mà decal này sẽ chiếu lên. Theo mặc định, Decal ảnh hưởng đến tất cả layer. Tùy chọn này cho phép bạn chỉ định loại object nào nhận Decal và loại nào không. Điều này đặc biệt hữu ích để đảm bảo các object động không vô tình nhận một Decal vốn dành cho địa hình bên dưới chúng.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_distance_fade_begin:

.. rst-class:: classref-property

:ref:`float<class_float>` **distance_fade_begin** = ``40.0`` :ref:`🔗<class_Decal_property_distance_fade_begin>`

.. rst-class:: classref-property-setget

- |void| **set_distance_fade_begin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_distance_fade_begin**\ (\ )

Khoảng cách tính từ camera tại đó Decal bắt đầu mờ dần (theo đơn vị 3D).

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_distance_fade_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **distance_fade_enabled** = ``false`` :ref:`🔗<class_Decal_property_distance_fade_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enable_distance_fade**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_distance_fade_enabled**\ (\ )

Nếu ``true``, decal sẽ mờ dần một cách mượt mà khi ở xa :ref:`Camera3D<class_Camera3D>` đang hoạt động, bắt đầu từ :ref:`distance_fade_begin<class_Decal_property_distance_fade_begin>`. Decal sẽ mờ dần trong phạm vi :ref:`distance_fade_begin<class_Decal_property_distance_fade_begin>` + :ref:`distance_fade_length<class_Decal_property_distance_fade_length>`, sau đó bị cull và hoàn toàn không được gửi đến shader. Sử dụng tùy chọn này để giảm số Decal đang hoạt động trong scene và nhờ đó cải thiện hiệu năng.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_distance_fade_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **distance_fade_length** = ``10.0`` :ref:`🔗<class_Decal_property_distance_fade_length>`

.. rst-class:: classref-property-setget

- |void| **set_distance_fade_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_distance_fade_length**\ (\ )

Khoảng cách mà Decal mờ dần (theo đơn vị 3D). Decal sẽ trở nên trong suốt hơn từ từ trong khoảng cách này và hoàn toàn vô hình ở cuối khoảng cách. Giá trị cao hơn tạo ra quá trình chuyển tiếp mờ dần mượt hơn, phù hợp hơn khi camera di chuyển nhanh.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_emission_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_energy** = ``1.0`` :ref:`🔗<class_Decal_property_emission_energy>`

.. rst-class:: classref-property-setget

- |void| **set_emission_energy**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_energy**\ (\ )

Hệ số năng lượng cho texture emission. Tùy chọn này khiến decal phát sáng với cường độ cao hơn hoặc thấp hơn, độc lập với màu albedo. Xem thêm :ref:`modulate<class_Decal_property_modulate>`.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_lower_fade:

.. rst-class:: classref-property

:ref:`float<class_float>` **lower_fade** = ``0.3`` :ref:`🔗<class_Decal_property_lower_fade>`

.. rst-class:: classref-property-setget

- |void| **set_lower_fade**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lower_fade**\ (\ )

Thiết lập đường cong mà decal sẽ mờ dần khi bề mặt càng xa tâm của :ref:`AABB<class_AABB>`. Chỉ các giá trị dương mới hợp lệ (giá trị âm sẽ bị giới hạn thành ``0.0``). Xem thêm :ref:`upper_fade<class_Decal_property_upper_fade>`.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_modulate:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **modulate** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Decal_property_modulate>`

.. rst-class:: classref-property-setget

- |void| **set_modulate**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_modulate**\ (\ )

Thay đổi :ref:`Color<class_Color>` của Decal bằng cách nhân màu albedo và emission với giá trị này. Thành phần alpha chỉ được tính đến khi nhân màu albedo, không áp dụng cho màu emission. Xem thêm :ref:`emission_energy<class_Decal_property_emission_energy>` và :ref:`albedo_mix<class_Decal_property_albedo_mix>` để thay đổi cường độ emission và albedo độc lập với nhau.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_normal_fade:

.. rst-class:: classref-property

:ref:`float<class_float>` **normal_fade** = ``0.0`` :ref:`🔗<class_Decal_property_normal_fade>`

.. rst-class:: classref-property-setget

- |void| **set_normal_fade**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_normal_fade**\ (\ )

Làm mờ Decal nếu góc giữa :ref:`AABB<class_AABB>` của Decal và bề mặt đích trở nên quá lớn. Giá trị ``0`` sẽ chiếu Decal bất kể góc nào, còn giá trị ``1`` giới hạn Decal ở các bề mặt gần như vuông góc.

\ **Lưu ý:** Đặt :ref:`normal_fade<class_Decal_property_normal_fade>` thành giá trị lớn hơn ``0.0`` sẽ gây tốn hiệu năng một chút do phải thực hiện thêm các phép tính góc normal.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_Decal_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Thiết lập kích thước của :ref:`AABB<class_AABB>` được decal sử dụng. Tất cả các chiều phải được đặt thành giá trị lớn hơn 0 (nếu không, chúng sẽ bị giới hạn thành ``0.001``). AABB kéo dài từ ``-size/2`` đến ``size/2``.

\ **Lưu ý:** Để cải thiện hiệu quả culling của các decal "hard surface", hãy đặt :ref:`upper_fade<class_Decal_property_upper_fade>` và :ref:`lower_fade<class_Decal_property_lower_fade>` của chúng thành ``0.0`` và đặt thành phần Y của :ref:`size<class_Decal_property_size>` thấp nhất có thể. Điều này sẽ giảm kích thước AABB của decal mà không ảnh hưởng đến hình thức hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_texture_albedo:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture_albedo** :ref:`🔗<class_Decal_property_texture_albedo>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const|

:ref:`Texture2D<class_Texture2D>` với :ref:`Color<class_Color>` cơ sở của Decal. Phải đặt giá trị cho mục này hoặc :ref:`texture_emission<class_Decal_property_texture_emission>` thì Decal mới hiển thị. Sử dụng kênh alpha như một mask để blend mượt các cạnh của decal với object bên dưới.

\ **Lưu ý:** Không giống như :ref:`BaseMaterial3D<class_BaseMaterial3D>`, trong đó chế độ filter có thể được điều chỉnh theo từng material, chế độ filter cho texture **Decal** được thiết lập trên toàn cục bằng :ref:`ProjectSettings.rendering/textures/decals/filter<class_ProjectSettings_property_rendering/textures/decals/filter>`.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_texture_emission:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture_emission** :ref:`🔗<class_Decal_property_texture_emission>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const|

:ref:`Texture2D<class_Texture2D>` với :ref:`Color<class_Color>` phát sáng của Decal. Phải thiết lập mục này hoặc :ref:`texture_albedo<class_Decal_property_texture_albedo>` để Decal hiển thị. Sử dụng kênh alpha như một mặt nạ để hòa trộn mượt các cạnh của decal với đối tượng bên dưới.

\ **Lưu ý:** Không giống :ref:`BaseMaterial3D<class_BaseMaterial3D>`, trong đó chế độ lọc có thể được điều chỉnh theo từng material, chế độ lọc cho texture **Decal** được thiết lập trên toàn cục bằng :ref:`ProjectSettings.rendering/textures/decals/filter<class_ProjectSettings_property_rendering/textures/decals/filter>`.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_texture_normal:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture_normal** :ref:`🔗<class_Decal_property_texture_normal>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const|

:ref:`Texture2D<class_Texture2D>` với normal map theo từng pixel cho decal. Sử dụng mục này để thêm chi tiết cho decal.

\ **Lưu ý:** Không giống :ref:`BaseMaterial3D<class_BaseMaterial3D>`, trong đó chế độ lọc có thể được điều chỉnh theo từng material, chế độ lọc cho texture **Decal** được thiết lập trên toàn cục bằng :ref:`ProjectSettings.rendering/textures/decals/filter<class_ProjectSettings_property_rendering/textures/decals/filter>`.

\ **Lưu ý:** Chỉ thiết lập texture này sẽ không làm decal hiển thị, vì cũng phải thiết lập :ref:`texture_albedo<class_Decal_property_texture_albedo>`. Để tạo decal chỉ có normal, hãy tải texture albedo vào :ref:`texture_albedo<class_Decal_property_texture_albedo>` và đặt :ref:`albedo_mix<class_Decal_property_albedo_mix>` thành ``0.0``. Kênh alpha của texture albedo sẽ được sử dụng để xác định nơi normal map của bề mặt bên dưới sẽ bị ghi đè (và cường độ của nó).

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_texture_orm:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture_orm** :ref:`🔗<class_Decal_property_texture_orm>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const|

:ref:`Texture2D<class_Texture2D>` lưu trữ ambient occlusion, roughness và metallic cho decal. Sử dụng mục này để thêm chi tiết cho decal.

\ **Lưu ý:** Không giống :ref:`BaseMaterial3D<class_BaseMaterial3D>`, trong đó chế độ lọc có thể được điều chỉnh theo từng material, chế độ lọc cho texture **Decal** được thiết lập trên toàn cục bằng :ref:`ProjectSettings.rendering/textures/decals/filter<class_ProjectSettings_property_rendering/textures/decals/filter>`.

\ **Lưu ý:** Chỉ thiết lập texture này sẽ không làm decal hiển thị, vì cũng phải thiết lập :ref:`texture_albedo<class_Decal_property_texture_albedo>`. Để tạo decal chỉ có ORM, hãy tải texture albedo vào :ref:`texture_albedo<class_Decal_property_texture_albedo>` và đặt :ref:`albedo_mix<class_Decal_property_albedo_mix>` thành ``0.0``. Kênh alpha của texture albedo sẽ được sử dụng để xác định nơi ORM map của bề mặt bên dưới sẽ bị ghi đè (và cường độ của nó).

\ **Lưu ý:** Do các giới hạn kỹ thuật, việc thay đổi roughness của bề mặt bên dưới bằng :ref:`texture_orm<class_Decal_property_texture_orm>` *không* ảnh hưởng đến phản xạ trong không gian màn hình (:ref:`Environment.ssr_enabled<class_Environment_property_ssr_enabled>`), phản xạ từ :ref:`VoxelGI<class_VoxelGI>` và phản xạ từ SDFGI (:ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`). Chỉ các phản xạ từ :ref:`ReflectionProbe<class_ReflectionProbe>`\ s mới bị ảnh hưởng.

.. rst-class:: classref-item-separator

----

.. _class_Decal_property_upper_fade:

.. rst-class:: classref-property

:ref:`float<class_float>` **upper_fade** = ``0.3`` :ref:`🔗<class_Decal_property_upper_fade>`

.. rst-class:: classref-property-setget

- |void| **set_upper_fade**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_upper_fade**\ (\ )

Thiết lập đường cong mà theo đó decal sẽ mờ dần khi bề mặt cách xa hơn khỏi tâm của :ref:`AABB<class_AABB>`. Chỉ các giá trị dương mới hợp lệ (các giá trị âm sẽ được giới hạn về ``0.0``). Xem thêm :ref:`lower_fade<class_Decal_property_lower_fade>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Decal_method_get_texture:

.. rst-class:: classref-method

:ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`\ ) |const| :ref:`🔗<class_Decal_method_get_texture>`

Trả về :ref:`Texture2D<class_Texture2D>` liên kết với :ref:`DecalTexture<enum_Decal_DecalTexture>` được chỉ định. Đây là một convenience method; trong hầu hết trường hợp, bạn nên truy cập trực tiếp vào texture.

Ví dụ, thay vì ``albedo_tex = $Decal.get_texture(Decal.TEXTURE_ALBEDO)``, hãy sử dụng ``albedo_tex = $Decal.texture_albedo``.

Một trường hợp mà cách này tốt hơn việc truy cập trực tiếp vào texture là khi bạn muốn sao chép texture của một Decal sang một Decal khác. Ví dụ:


.. tabs::

 .. code-tab:: gdscript

    for i in Decal.TEXTURE_MAX:
        $NewDecal.set_texture(i, $OldDecal.get_texture(i))

 .. code-tab:: csharp

    for (int i = 0; i < (int)Decal.DecalTexture.Max; i++)
    {
        GetNode<Decal>("NewDecal").SetTexture(i, GetNode<Decal>("OldDecal").GetTexture(i));
    }



.. rst-class:: classref-item-separator

----

.. _class_Decal_method_set_texture:

.. rst-class:: classref-method

|void| **set_texture**\ (\ type\: :ref:`DecalTexture<enum_Decal_DecalTexture>`, texture\: :ref:`Texture2D<class_Texture2D>`\ ) :ref:`🔗<class_Decal_method_set_texture>`

Thiết lập :ref:`Texture2D<class_Texture2D>` liên kết với :ref:`DecalTexture<enum_Decal_DecalTexture>` được chỉ định. Đây là một convenience method; trong hầu hết trường hợp, bạn nên truy cập trực tiếp vào texture.

Ví dụ, thay vì ``$Decal.set_texture(Decal.TEXTURE_ALBEDO, albedo_tex)``, hãy sử dụng ``$Decal.texture_albedo = albedo_tex``.

Một trường hợp mà cách này tốt hơn việc truy cập trực tiếp vào texture là khi bạn muốn sao chép texture của một Decal sang một Decal khác. Ví dụ:


.. tabs::

 .. code-tab:: gdscript

    for i in Decal.TEXTURE_MAX:
        $NewDecal.set_texture(i, $OldDecal.get_texture(i))

 .. code-tab:: csharp

    for (int i = 0; i < (int)Decal.DecalTexture.Max; i++)
    {
        GetNode<Decal>("NewDecal").SetTexture(i, GetNode<Decal>("OldDecal").GetTexture(i));
    }



.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
