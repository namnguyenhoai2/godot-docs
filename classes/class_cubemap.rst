:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Cubemap.xml.

.. _class_Cubemap:

Cubemap
=======

**Kế thừa:** :ref:`ImageTextureLayered<class_ImageTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Sáu texture hình vuông đại diện cho các mặt của một khối lập phương. Thường được dùng làm skybox.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một cubemap gồm 6 texture được sắp xếp theo các layer. Chúng thường được dùng để giả lập phản chiếu trong kết xuất 3D (xem :ref:`ReflectionProbe<class_ReflectionProbe>`). Nó có thể khiến một đối tượng trông như đang phản chiếu môi trường xung quanh. Cách này thường mang lại hiệu năng tốt hơn nhiều so với các phương pháp phản chiếu khác.

Resource này thường được dùng làm uniform trong custom shader. Một số ít phương thức cốt lõi của Godot sử dụng resource **Cubemap**.

Để tự tạo một tệp texture như vậy, hãy reimport các tệp hình ảnh bằng import preset của Godot Editor. Để tạo một Cubemap từ code, hãy dùng :ref:`ImageTextureLayered.create_from_images()<class_ImageTextureLayered_method_create_from_images>` trên một instance của class Cubemap.

Thứ tự hình ảnh dự kiến là X+, X-, Y+, Y-, Z+, Z- (theo hệ tọa độ của Godot, vì vậy Y+ là "lên" và Z- là "tiến về phía trước"). Bạn có thể dùng một trong các template sau làm cơ sở:

- `2×3 cubemap template (default layout option) <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_2x3.webp>`__\

- `3×2 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_3x2.webp>`__\

- `1×6 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_1x6.webp>`__\

- `6×1 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_6x1.webp>`__\

\ **Lưu ý:** Godot không hỗ trợ sử dụng cubemap trong một :ref:`PanoramaSkyMaterial<class_PanoramaSkyMaterial>`. Để dùng cubemap làm skybox, hãy chuyển đổi :ref:`PanoramaSkyMaterial<class_PanoramaSkyMaterial>` mặc định thành :ref:`ShaderMaterial<class_ShaderMaterial>` bằng tùy chọn resource **Convert to ShaderMaterial** trong dropdown, sau đó thay code của nó bằng nội dung sau:

.. code:: text

    shader_type sky;

    uniform samplerCube source_panorama : filter_linear, source_color, hint_default_black;
    uniform float exposure : hint_range(0, 128) = 1.0;

    void sky() {
        // Nếu import một cubemap từ engine khác, bạn có thể cần lật một trong các component `EYEDIR` bên dưới
        // bằng cách thay thế nó bằng `-EYEDIR`.
        vec3 eyedir = vec3(EYEDIR.x, EYEDIR.y, EYEDIR.z);
        COLOR = texture(source_panorama, eyedir).rgb * exposure;
    }

Sau khi thay code shader và lưu, hãy chỉ định resource Cubemap đã import trong phần Shader Parameters của ShaderMaterial ở inspector.

Ngoài ra, bạn có thể dùng `this tool <https://danilw.github.io/GLSL-howto/cubemap_to_panorama_js/cubemap_to_panorama.html>`__ để chuyển đổi cubemap thành sky map equirectangular và dùng :ref:`PanoramaSkyMaterial<class_PanoramaSkyMaterial>` như thường lệ.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>` | :ref:`create_placeholder<class_Cubemap_method_create_placeholder>`\ (\ ) |const| |
   +---------------------------------+----------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Cubemap_method_create_placeholder:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **create_placeholder**\ (\ ) |const| :ref:`🔗<class_Cubemap_method_create_placeholder>`

Tạo một phiên bản placeholder của resource này (:ref:`PlaceholderCubemap<class_PlaceholderCubemap>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
