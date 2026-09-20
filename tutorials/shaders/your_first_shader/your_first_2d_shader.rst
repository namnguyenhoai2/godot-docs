.. _doc_your_first_canvasitem_shader:

Shader 2D đầu tiên của bạn
==========================

Giới thiệu
----------

Shader là những chương trình đặc biệt thực thi trên GPU và được dùng để render đồ họa. Mọi hoạt động rendering hiện đại đều được thực hiện bằng shader. Để xem mô tả chi tiết hơn về shader, vui lòng xem :ref:`What are shaders <doc_introduction_to_shaders>`.

Tutorial này tập trung vào các khía cạnh thực tiễn của việc viết chương trình shader bằng cách hướng dẫn bạn qua quy trình viết một shader với cả các hàm vertex và fragment. Tutorial này dành cho những người hoàn toàn mới làm quen với shader.

.. note:: If you have experience writing shaders and are just looking for an
          tổng quan về cách shader hoạt động trong Godot, hãy xem :ref:`Shading Reference <toc-shading-reference>`.

Thiết lập
---------

:ref:`CanvasItem shaders <doc_canvas_item_shader>` are used to draw all 2D
các object trong Godot, còn shader :ref:`Spatial <doc_spatial_shader>` được dùng để vẽ tất cả object 3D.

Để sử dụng shader, shader phải được gắn vào một :ref:`Material <class_Material>`, và resource này phải được gắn vào một object. Material là một loại
:ref:`Resource <doc_resources>`. To draw multiple objects with the same
material, material phải được gắn vào từng object.

Tất cả object kế thừa từ :ref:`CanvasItem <class_CanvasItem>` đều có thuộc tính material. Điều này bao gồm tất cả :ref:`GUI elements <class_Control>`, :ref:`Sprite2Ds <class_Sprite2D>`, :ref:`TileMapLayers <class_TileMapLayer>`, :ref:`MeshInstance2Ds <class_MeshInstance2D>`, v.v. Chúng cũng có tùy chọn kế thừa material của node cha. Điều này hữu ích khi bạn có một số lượng lớn node muốn sử dụng cùng một material.

Để bắt đầu, hãy tạo một node Sprite2D. :ref:`You can use any CanvasItem <doc_custom_drawing_in_2d>`, miễn là nó đang vẽ lên canvas, vì vậy trong tutorial này chúng ta sẽ dùng Sprite2D, do đây là CanvasItem dễ bắt đầu vẽ nhất.

Trong Inspector, nhấp bên cạnh "Texture", tại chỗ hiển thị "[empty]", rồi chọn "Load", sau đó chọn "icon.svg". Với các project mới, đây là icon Godot. Bây giờ bạn sẽ thấy icon trong viewport.

Tiếp theo, nhìn xuống Inspector, trong phần CanvasItem, nhấp bên cạnh "Material" và chọn "New ShaderMaterial". Thao tác này tạo một resource Material mới. Nhấp vào hình cầu xuất hiện. Hiện tại Godot chưa biết bạn đang viết CanvasItem Shader hay Spatial Shader, và nó xem trước output của spatial shader. Vì vậy, thứ bạn đang thấy là output của Spatial Shader mặc định.

.. note::
  Các material kế thừa từ resource :ref:`class_Material`, chẳng hạn như :ref:`class_StandardMaterial3D` và :ref:`class_ParticleProcessMaterial`, có thể được chuyển đổi thành :ref:`class_ShaderMaterial`, đồng thời các thuộc tính hiện có của chúng sẽ được chuyển đổi thành một text shader đi kèm. Để thực hiện, hãy nhấp chuột phải vào material trong dock FileSystem và chọn **Convert to ShaderMaterial**. Bạn cũng có thể thực hiện việc này bằng cách nhấp chuột phải vào bất kỳ thuộc tính nào trong inspector đang chứa tham chiếu đến material.

Nhấp bên cạnh "Shader" và chọn "New Shader". Cuối cùng, nhấp vào shader bạn vừa tạo để mở shader editor. Bây giờ bạn đã sẵn sàng bắt đầu viết shader đầu tiên của mình.

CanvasItem shader đầu tiên của bạn
----------------------------------

Trong Godot, mọi shader đều bắt đầu bằng một dòng chỉ rõ loại shader. Dòng này có định dạng sau:

.. code-block:: glsl

  shader_type canvas_item;

Vì chúng ta đang viết CanvasItem shader, nên ở dòng đầu tiên, chúng ta chỉ định ``canvas_item``. Toàn bộ code của chúng ta sẽ nằm bên dưới khai báo này.

Dòng này cho engine biết những biến built-in và chức năng nào cần cung cấp cho bạn.

Trong Godot, bạn có thể override ba hàm để điều khiển cách shader hoạt động; ``vertex``, ``fragment`` và ``light``. Tutorial này sẽ hướng dẫn bạn viết một shader với cả các hàm vertex và fragment. Các hàm light phức tạp hơn đáng kể so với các hàm vertex và fragment, vì vậy sẽ không được đề cập ở đây.

Hàm fragment đầu tiên của bạn
-----------------------------

Hàm fragment chạy cho từng pixel trong một Sprite2D và xác định pixel đó nên có màu gì.

Chúng chỉ bị giới hạn trong các pixel được Sprite2D bao phủ, điều đó có nghĩa là bạn không thể dùng chúng để, chẳng hạn, tạo đường viền quanh một Sprite2D.

Hàm fragment cơ bản nhất không làm gì ngoài việc gán một màu duy nhất cho mọi pixel.

Chúng ta thực hiện việc này bằng cách viết một ``vec4`` vào biến built-in ``COLOR``. ``vec4`` là cách viết tắt để tạo một vector gồm 4 số. Để biết thêm thông tin về vector, hãy xem :ref:`Vector math tutorial <doc_vector_math>`. ``COLOR`` vừa là một biến input của hàm fragment, vừa là output cuối cùng của hàm đó.

.. code-block:: glsl

  void fragment(){
    COLOR = vec4(0.4, 0.6, 0.9, 1.0);
  }

.. image:: img/blue-box.png

Chúc mừng! Bạn đã hoàn thành. Bạn đã viết thành công shader đầu tiên trong Godot.

Bây giờ hãy làm mọi thứ phức tạp hơn.

Có nhiều input cho hàm fragment mà bạn có thể dùng để tính toán ``COLOR``. ``UV`` là một trong số đó. Tọa độ UV được chỉ định trong Sprite2D của bạn (mà bạn không hề biết!) và cho shader biết cần đọc từ texture ở đâu cho từng phần của mesh.

Trong hàm fragment, bạn chỉ có thể đọc từ ``UV``, nhưng bạn có thể sử dụng nó trong các hàm khác hoặc gán trực tiếp các giá trị cho ``COLOR``.

``UV`` thay đổi từ 0-1 theo chiều trái-phải và từ trên xuống dưới.

.. image:: img/iconuv.png

.. code-block:: glsl

  void fragment() {
    COLOR = vec4(UV, 0.5, 1.0);
  }

.. image:: img/UV.png

Sử dụng biến built-in ``TEXTURE``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hàm fragment mặc định đọc từ texture Sprite2D đã được thiết lập và hiển thị texture đó.

Khi muốn điều chỉnh màu của một Sprite2D, bạn có thể điều chỉnh thủ công màu từ texture như trong đoạn code dưới đây.

.. code-block:: glsl

  void fragment(){
    // Shader này sẽ tạo ra một icon có sắc xanh lam
    COLOR.b = 1.0;
  }

Một số node, chẳng hạn như Sprite2D, có một biến texture chuyên dụng mà bạn có thể truy cập trong shader bằng ``TEXTURE``. Nếu muốn sử dụng texture Sprite2D để kết hợp với các màu khác, bạn có thể dùng ``UV`` cùng với hàm ``texture`` để truy cập biến này. Hãy dùng chúng để vẽ lại Sprite2D bằng texture.

.. code-block:: glsl

  void fragment(){
    COLOR = texture(TEXTURE, UV); // Đọc lại từ texture.
    COLOR.b = 1.0; //đặt kênh blue thành 1.0
  }

.. image:: img/blue-tex.png

Input uniform
~~~~~~~~~~~~~

Input uniform được dùng để truyền dữ liệu vào shader, và dữ liệu này sẽ giống nhau trong toàn bộ shader.

Bạn có thể sử dụng uniform bằng cách định nghĩa chúng ở đầu shader như sau:

.. code-block:: glsl

  uniform float size;

Để biết thêm thông tin về cách sử dụng, hãy xem :ref:`Shading Language doc <doc_shading_language>`.

Thêm một uniform để thay đổi mức blue trong Sprite2D của chúng ta.

.. code-block:: glsl

  uniform float blue = 1.0; // bạn có thể gán giá trị mặc định cho uniform

  void fragment(){
    COLOR = texture(TEXTURE, UV); // Đọc từ texture
    COLOR.b = blue;
  }

Bây giờ bạn có thể thay đổi mức blue trong Sprite2D từ editor. Hãy nhìn lại Inspector, bên dưới nơi bạn đã tạo shader. Bạn sẽ thấy một phần có tên "Shader Param". Mở rộng phần đó và bạn sẽ thấy uniform vừa khai báo. Nếu thay đổi giá trị trong editor, giá trị đó sẽ ghi đè lên giá trị mặc định bạn đã cung cấp trong shader.

Tương tác với shader từ code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể thay đổi uniform từ code bằng hàm ``set_shader_parameter()``, được gọi trên resource material của node. Với một node Sprite2D, bạn có thể sử dụng đoạn code sau để thiết lập uniform ``blue``.

.. tabs::

 .. code-tab:: gdscript

  var blue_value = 1.0
  material.set_shader_parameter("blue", blue_value)

 .. code-tab:: csharp

  var blueValue = 1.0;
  ((ShaderMaterial)Material).SetShaderParameter("blue", blueValue);

Lưu ý rằng tên của uniform là một string. String này phải khớp chính xác với cách nó được viết trong shader, bao gồm cả chính tả và kiểu chữ.

Hàm vertex đầu tiên của bạn
---------------------------

Bây giờ chúng ta đã có một hàm fragment, hãy viết một hàm vertex.

Sử dụng hàm vertex để tính toán vị trí cuối cùng của từng vertex trên màn hình.

Biến quan trọng nhất trong hàm vertex là ``VERTEX``. Ban đầu, nó chỉ định tọa độ vertex trong model, nhưng bạn cũng ghi vào nó để xác định vị trí thực sự cần vẽ các vertex đó. ``VERTEX`` là một ``vec2``, ban đầu được biểu diễn trong local-space (tức là không tương đối với camera, viewport hoặc các node cha).

Bạn có thể offset các vertex bằng cách cộng trực tiếp vào ``VERTEX``.

.. code-block:: glsl

  void vertex() {
    VERTEX += vec2(10.0, 0.0);
  }

Kết hợp với biến built-in ``TIME``, cách này có thể được dùng cho animation cơ bản.

.. code-block:: glsl

  void vertex() {
    // Animate Sprite2D chuyển động theo một vòng tròn lớn quanh vị trí của nó
    VERTEX += vec2(cos(TIME)*100.0, sin(TIME)*100.0);
  }

Kết luận
--------

Về bản chất, shader thực hiện những gì bạn đã thấy, đó là tính toán ``VERTEX`` và ``COLOR``. Việc nghĩ ra các chiến lược toán học phức tạp hơn để gán giá trị cho những biến đó là tùy thuộc vào bạn.

Để tìm cảm hứng, hãy xem một số tutorial shader nâng cao hơn và tham khảo các trang khác như `Shadertoy <https://www.shadertoy.com/results?query=&sort=popular&from=10&num=4>`_ và `The Book of Shaders <https://thebookofshaders.com>`_.
