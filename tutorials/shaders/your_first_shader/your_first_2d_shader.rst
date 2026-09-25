.. _doc_your_first_canvasitem_shader:

Shader 2D đầu tiên của bạn
==========================

Giới thiệu
----------

Shader là những chương trình đặc biệt chạy trên GPU và được dùng để kết xuất đồ họa. Mọi hoạt động kết xuất hiện đại đều được thực hiện bằng shader. Để xem mô tả chi tiết hơn về shader, hãy xem :ref:`What are shaders <doc_introduction_to_shaders>`.

Tutorial này tập trung vào các khía cạnh thực tiễn của việc viết chương trình shader bằng cách hướng dẫn bạn từng bước viết một shader với cả hàm vertex và fragment. Tutorial này dành cho những người hoàn toàn mới làm quen với shader.

.. note:: Nếu bạn đã có kinh nghiệm viết shader và chỉ muốn xem tổng quan về cách shader hoạt động trong Godot, hãy xem :ref:`Shading Reference <toc-shading-reference>`.

Thiết lập
---------

:ref:`CanvasItem shaders <doc_canvas_item_shader>` được dùng để vẽ tất cả đối tượng 2D trong Godot, còn shader :ref:`Spatial <doc_spatial_shader>` được dùng để vẽ tất cả đối tượng 3D.

Để sử dụng shader, shader phải được gắn vào một :ref:`Material <class_Material>` và đối tượng đó cũng phải được gắn vào một đối tượng. Material là một loại
:ref:`Resource <doc_resources>`. Để vẽ nhiều đối tượng bằng cùng một material, material phải được gắn vào từng đối tượng.

Tất cả đối tượng dẫn xuất từ :ref:`CanvasItem <class_CanvasItem>` đều có thuộc tính material. Điều này bao gồm mọi phần tử :ref:`GUI elements <class_Control>`, :ref:`Sprite2Ds <class_Sprite2D>`, :ref:`TileMapLayers <class_TileMapLayer>`, :ref:`MeshInstance2Ds <class_MeshInstance2D>` v.v. Chúng cũng có tùy chọn kế thừa material của node cha. Tùy chọn này hữu ích khi bạn có nhiều node muốn sử dụng cùng một material.

Để bắt đầu, hãy tạo một node Sprite2D. :ref:`You can use any CanvasItem <doc_custom_drawing_in_2d>`, miễn là nó đang vẽ lên canvas, nên trong tutorial này chúng ta sẽ dùng một Sprite2D vì đây là CanvasItem dễ bắt đầu vẽ nhất.

Trong Inspector, nhấp bên cạnh "Texture" tại chỗ hiển thị "[empty]" rồi chọn "Load", sau đó chọn "icon.svg". Với các dự án mới, đây là biểu tượng Godot. Bây giờ bạn sẽ thấy biểu tượng trong viewport.

Tiếp theo, nhìn xuống Inspector, trong phần CanvasItem, nhấp bên cạnh "Material" và chọn "New ShaderMaterial". Thao tác này tạo một tài nguyên Material mới. Nhấp vào hình cầu xuất hiện. Hiện tại Godot chưa biết bạn đang viết CanvasItem Shader hay Spatial Shader và đang xem trước đầu ra của spatial shader. Vì vậy, thứ bạn đang thấy là đầu ra của Spatial Shader mặc định.

.. note::
  Các material kế thừa từ tài nguyên :ref:`class_Material`, chẳng hạn như :ref:`class_StandardMaterial3D` và :ref:`class_ParticleProcessMaterial`, có thể được chuyển đổi thành :ref:`class_ShaderMaterial` và các thuộc tính hiện có của chúng sẽ được chuyển đổi thành một text shader đi kèm. Để thực hiện, hãy nhấp chuột phải vào material trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện việc này bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào đang chứa tham chiếu đến material trong Inspector.

Nhấp bên cạnh "Shader" và chọn "New Shader". Cuối cùng, nhấp vào shader bạn vừa tạo để mở shader editor. Bây giờ bạn đã sẵn sàng bắt đầu viết shader đầu tiên của mình.

Shader CanvasItem đầu tiên của bạn
----------------------------------

Trong Godot, mọi shader đều bắt đầu bằng một dòng chỉ rõ loại shader. Dòng này có định dạng sau:

.. code-block:: glsl

  shader_type canvas_item;

Vì chúng ta đang viết một CanvasItem shader, nên chỉ định ``canvas_item`` ở dòng đầu tiên. Toàn bộ mã của chúng ta sẽ nằm bên dưới khai báo này.

Dòng này cho engine biết những biến dựng sẵn và chức năng nào cần cung cấp cho bạn.

Trong Godot, bạn có thể ghi đè ba hàm để kiểm soát cách shader hoạt động: ``vertex``, ``fragment`` và ``light``. Tutorial này sẽ hướng dẫn bạn viết một shader với cả hàm vertex và fragment. Các hàm light phức tạp hơn đáng kể so với hàm vertex và fragment, vì vậy sẽ không được đề cập ở đây.

Hàm fragment đầu tiên của bạn
-----------------------------

Hàm fragment chạy cho từng pixel trong một Sprite2D và xác định pixel đó nên có màu gì.

Chúng bị giới hạn trong các pixel được Sprite2D bao phủ, nghĩa là bạn không thể dùng hàm này để, chẳng hạn, tạo đường viền quanh một Sprite2D.

Hàm fragment cơ bản nhất không làm gì ngoài việc gán một màu duy nhất cho mọi pixel.

Chúng ta thực hiện việc này bằng cách viết một ``vec4`` vào biến dựng sẵn ``COLOR``. ``vec4`` là cách viết tắt để tạo một vector gồm 4 số. Để biết thêm thông tin về vector, hãy xem :ref:`Vector math tutorial <doc_vector_math>`. ``COLOR`` vừa là biến đầu vào của hàm fragment, vừa là đầu ra cuối cùng của hàm này.

.. code-block:: glsl

  void fragment(){
    COLOR = vec4(0.4, 0.6, 0.9, 1.0);
  }

.. image:: img/blue-box.png

Chúc mừng! Bạn đã hoàn tất. Bạn đã viết thành công shader đầu tiên trong Godot.

Bây giờ hãy làm cho mọi thứ phức tạp hơn.

Hàm fragment có nhiều đầu vào mà bạn có thể sử dụng để tính toán ``COLOR``. ``UV`` là một trong số đó. Tọa độ UV được chỉ định trong Sprite2D (mà bạn không cần biết!) và cho shader biết cần đọc từ texture ở đâu đối với từng phần của mesh.

Trong hàm fragment, bạn chỉ có thể đọc từ ``UV``, nhưng có thể sử dụng nó trong các hàm khác hoặc gán trực tiếp các giá trị cho ``COLOR``.

``UV`` thay đổi từ 0 đến 1 theo chiều trái-phải và từ trên xuống dưới.

.. image:: img/iconuv.png

.. code-block:: glsl

  void fragment() {
    COLOR = vec4(UV, 0.5, 1.0);
  }

.. image:: img/UV.png

Sử dụng built-in ``TEXTURE``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hàm fragment mặc định đọc từ texture Sprite2D đã thiết lập và hiển thị texture đó.

Khi muốn điều chỉnh màu của một Sprite2D, bạn có thể điều chỉnh thủ công màu lấy từ texture như trong đoạn mã dưới đây.

.. code-block:: glsl

  void fragment(){
    // Shader này sẽ tạo ra một biểu tượng có sắc xanh lam
    COLOR.b = 1.0;
  }

Một số node, chẳng hạn như Sprite2D, có một biến texture chuyên dụng có thể được truy cập trong shader bằng ``TEXTURE``. Nếu muốn sử dụng texture của Sprite2D để kết hợp với các màu khác, bạn có thể dùng ``UV`` cùng với hàm ``texture`` để truy cập biến này. Hãy dùng chúng để vẽ lại Sprite2D bằng texture.

.. code-block:: glsl

  void fragment(){
    COLOR = texture(TEXTURE, UV); // Đọc lại từ texture.
    COLOR.b = 1.0; //đặt kênh màu xanh lam thành 1.0
  }

.. image:: img/blue-tex.png

Đầu vào uniform
~~~~~~~~~~~~~~~

Đầu vào uniform được dùng để truyền dữ liệu vào shader, dữ liệu này sẽ giống nhau trên toàn bộ shader.

Bạn có thể sử dụng uniform bằng cách định nghĩa chúng ở đầu shader như sau:

.. code-block:: glsl

  uniform float size;

Để biết thêm thông tin về cách sử dụng, hãy xem :ref:`Shading Language doc <doc_shading_language>`.

Thêm một uniform để thay đổi mức độ xanh lam trong Sprite2D.

.. code-block:: glsl

  uniform float blue = 1.0; // bạn có thể gán giá trị mặc định cho uniform

  void fragment(){
    COLOR = texture(TEXTURE, UV); // Đọc từ texture
    COLOR.b = blue;
  }

Giờ đây, bạn có thể thay đổi lượng màu xanh dương trong Sprite2D từ editor. Hãy xem lại Inspector, bên dưới nơi bạn đã tạo shader. Bạn sẽ thấy một mục có tên "Shader Param". Mở rộng mục đó và bạn sẽ thấy uniform vừa khai báo. Nếu thay đổi giá trị trong editor, giá trị đó sẽ ghi đè lên giá trị mặc định bạn đã cung cấp trong shader.

Tương tác với shader từ code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể thay đổi uniform từ code bằng hàm ``set_shader_parameter()``, được gọi trên material resource của node. Với một node Sprite2D, bạn có thể sử dụng đoạn code sau để đặt uniform ``blue``.

.. tabs::

 .. code-tab:: gdscript

  var blue_value = 1.0
  material.set_shader_parameter("blue", blue_value)

 .. code-tab:: csharp

  var blueValue = 1.0;
  ((ShaderMaterial)Material).SetShaderParameter("blue", blueValue);

Lưu ý rằng tên của uniform là một chuỗi. Chuỗi này phải khớp chính xác với cách nó được viết trong shader, bao gồm cả chính tả và kiểu chữ.

Hàm vertex đầu tiên của bạn
---------------------------

Bây giờ chúng ta đã có một hàm fragment, hãy viết một hàm vertex.

Sử dụng hàm vertex để tính toán vị trí trên màn hình mà mỗi vertex sẽ được đặt vào.

Biến quan trọng nhất trong hàm vertex là ``VERTEX``. Ban đầu, nó chỉ định tọa độ vertex trong model của bạn, nhưng bạn cũng ghi dữ liệu vào đó để xác định vị trí thực tế cần vẽ các vertex. ``VERTEX`` là một ``vec2`` ban đầu được biểu diễn trong local-space (tức là không tương đối với camera, viewport hoặc các node cha).

Bạn có thể dịch chuyển các vertex bằng cách cộng trực tiếp vào ``VERTEX``.

.. code-block:: glsl

  void vertex() {
    VERTEX += vec2(10.0, 0.0);
  }

Kết hợp với biến built-in ``TIME``, bạn có thể dùng cách này để tạo animation cơ bản.

.. code-block:: glsl

  void vertex() {
    // Tạo hiệu ứng Sprite2D chuyển động theo một vòng tròn lớn quanh vị trí của nó
    VERTEX += vec2(cos(TIME)*100.0, sin(TIME)*100.0);
  }

Kết luận
--------

Về cốt lõi, shader thực hiện những gì bạn đã thấy cho đến nay: tính toán ``VERTEX`` và ``COLOR``. Bạn có thể tự nghĩ ra những chiến lược toán học phức tạp hơn để gán giá trị cho các biến đó.

Để tìm cảm hứng, hãy xem một số tutorial shader nâng cao hơn và tham khảo các trang khác như `Shadertoy <https://www.shadertoy.com/results?query=&sort=popular&from=10&num=4>`_ và `The Book of Shaders <https://thebookofshaders.com>`_.

.. _`Shadertoy`: https://www.shadertoy.com/results?query=&sort=popular&from=10&num=4
.. _`The Book of Shaders`: https://thebookofshaders.com
