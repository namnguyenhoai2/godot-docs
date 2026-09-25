.. _doc_visual_shaders:

Sử dụng VisualShaders
=====================

VisualShaders là giải pháp trực quan thay thế cho việc tạo shader.

Vì shader vốn gắn liền với hình ảnh, cách tiếp cận dựa trên graph cùng các bản xem trước của texture, material, v.v. mang lại nhiều tiện lợi hơn so với shader hoàn toàn dựa trên script. Mặt khác, VisualShaders không cung cấp tất cả các tính năng của shader script, và có thể cần sử dụng song song cả hai để tạo ra những hiệu ứng cụ thể.

.. note::

    Nếu bạn chưa quen với shader, trước tiên hãy đọc
    :ref:`doc_introduction_to_shaders`.

Tạo một VisualShader
--------------------

Có thể tạo VisualShader trong bất kỳ :ref:`class_ShaderMaterial` nào. Để bắt đầu sử dụng VisualShader, hãy tạo một ``ShaderMaterial`` mới trong một đối tượng tùy ý.

.. image:: img/shader_material_create_mesh.webp

Sau đó, gán một resource :ref:`class_Shader` cho thuộc tính ``Shader``.

.. image:: img/visual_shader_create.webp

Nhấp vào resource ``Shader`` mới, hộp thoại Create Shader sẽ tự động mở. Đổi tùy chọn Type thành :ref:`class_VisualShader` trong menu thả xuống, sau đó đặt tên cho nó.

.. image:: img/visual_shader_create2.webp

Nhấp vào visual shader vừa tạo để mở Shader Editor. Bố cục của Shader Editor gồm bốn phần: danh sách tệp ở bên trái, thanh công cụ phía trên, graph và bản xem trước material ở bên phải, có thể tắt

.. image:: img/visual_shader_editor2.webp

Từ trái sang phải trên thanh công cụ:

- Mũi tên có thể được dùng để bật hoặc tắt khả năng hiển thị của bảng tệp.
- Nút ``File`` mở menu thả xuống để lưu, tải và tạo tệp.
- Nút ``Add Node`` hiển thị menu bật lên, cho phép bạn thêm node vào shader graph.
- Menu thả xuống là loại shader: Vertex, Fragment và Light. Giống như với script shader, nó xác định những node dựng sẵn nào sẽ khả dụng.
- Các nút sau đây và ô nhập số điều khiển mức thu phóng, thao tác căn theo lưới và khoảng cách giữa các đường lưới (tính bằng pixel).
- Công tắc này điều khiển việc minimap của graph ở góc dưới bên phải của trình chỉnh sửa có hiển thị hay không.
- Nút tự động sắp xếp các node đã chọn sẽ cố gắng sắp xếp mọi node bạn đã chọn một cách hiệu quả và gọn gàng nhất có thể.
- Nút Manage Varyings mở menu thả xuống, cho phép bạn thêm hoặc xóa một varying.
- Nút hiển thị mã được tạo sẽ hiển thị shader code tương ứng với graph của bạn.
- Công tắc này bật hoặc tắt bản xem trước material.
- Nút ``Online Docs`` mở trang tài liệu này trong trình duyệt web.
- Nút cuối cùng cho phép bạn đặt shader editor trong một cửa sổ riêng, tách biệt với phần còn lại của trình chỉnh sửa.

.. note::

    Mặc dù VisualShaders không yêu cầu viết code, chúng có chung logic với script shader. Bạn nên học những kiến thức cơ bản của cả hai để hiểu rõ pipeline shading.

    Visual shader graph được chuyển đổi thành script shader ở phía sau, và bạn có thể xem mã này bằng cách nhấn nút cuối cùng trên thanh công cụ. Điều này có thể hữu ích để hiểu một node nhất định thực hiện điều gì và cách tái tạo node đó trong script.

Sử dụng Visual Shader Editor
----------------------------

Theo mặc định, mọi ``VisualShader`` mới đều có một output node. Mọi kết nối node đều kết thúc tại một trong các socket của output node. Node là đơn vị cơ bản để tạo shader. Để thêm node mới, hãy nhấp vào nút ``Add Node`` ở góc trên bên trái hoặc nhấp chuột phải vào bất kỳ vị trí trống nào trong graph; một menu sẽ bật lên.

.. image:: img/vs_popup.webp

Menu bật lên này có các đặc điểm sau:

- Nếu bạn nhấp chuột phải vào graph, menu này sẽ được gọi tại vị trí con trỏ và node được tạo trong trường hợp đó cũng sẽ được đặt bên dưới vị trí ấy; nếu không, node sẽ được tạo ở giữa graph.
- Bạn có thể thay đổi kích thước theo chiều ngang và chiều dọc để hiển thị thêm nội dung. Kích thước và vị trí nội dung của cây được lưu lại giữa các lần mở, vì vậy nếu bạn vô tình đóng menu bật lên, bạn có thể dễ dàng khôi phục trạng thái trước đó.
- Có thể sử dụng các tùy chọn ``Expand All`` và ``Collapse All`` trong menu tùy chọn thả xuống để dễ dàng liệt kê các node khả dụng.
- Bạn cũng có thể kéo và thả node từ menu bật lên vào graph.

Mặc dù các node trong menu bật lên được sắp xếp theo danh mục, lúc đầu chúng có thể khiến bạn choáng ngợp. Hãy thử thêm một số node, kết nối chúng với output socket và quan sát điều gì xảy ra.

Khi kết nối bất kỳ output ``scalar`` nào với input ``vector``, tất cả các thành phần của vector sẽ nhận giá trị của scalar.

Khi kết nối bất kỳ output ``vector`` nào với input ``scalar``, giá trị của scalar sẽ là giá trị trung bình của các thành phần trong vector.

Giao diện node Visual Shader
----------------------------

Các node visual shader có các cổng input và output. Các cổng input nằm ở bên trái node, còn các cổng output nằm ở bên phải node.

.. figure:: img/vs_node.webp

Các cổng này được tô màu để phân biệt loại cổng:

.. |scalar| image:: img/vs_scalar.webp
.. |vector| image:: img/vs_vector.webp
.. |boolean| image:: img/vs_boolean.webp
.. |transform| image:: img/vs_transform.webp
.. |sampler| image:: img/vs_sampler.webp


.. list-table:: Loại cổng
   :widths: auto
   :header-rows: 1

   * - Loại
     - Màu
     - Mô tả
     - Ví dụ
   * - Scalar
     - Xám
     - Scalar là một giá trị đơn.
     - |scalar|
   * - Vector
     - Tím
     - Vector là một tập hợp các giá trị.
     - |vector|
   * - Boolean
     - Xanh lục
     - Bật hoặc tắt, true hoặc false.
     - |boolean|
   * - Transform
     - Hồng
     - Một ma trận, thường được dùng để biến đổi các vertex.
     - |transform|
   * - Sampler
     - Cam
     - Một texture sampler. Nó có thể được dùng để lấy mẫu texture.
     - |sampler|

Tất cả các kiểu này đều được sử dụng trong phép tính của vertex, fragment và light trong shader. Ví dụ: phép nhân ma trận, phép cộng vector hoặc phép chia scalar.

Còn có những kiểu khác, nhưng đây là các kiểu chính.

Các node của Visual Shader
--------------------------

Dưới đây là một số node đặc biệt đáng biết. Danh sách này không đầy đủ và có thể được mở rộng thêm với nhiều node và ví dụ hơn.

Nút Expression
~~~~~~~~~~~~~~

Node ``Expression`` cho phép bạn viết các biểu thức bằng Godot Shading Language (tương tự GLSL) bên trong visual shader. Node này có các nút để thêm số lượng cổng đầu vào và đầu ra tùy ý, đồng thời có thể thay đổi kích thước. Bạn cũng có thể thiết lập tên và kiểu của từng cổng. Biểu thức bạn nhập sẽ được áp dụng ngay lập tức cho material (sau khi tiêu điểm rời khỏi hộp văn bản biểu thức). Mọi lỗi phân tích cú pháp hoặc biên dịch sẽ được in ra tab Output. Theo mặc định, các đầu ra được khởi tạo bằng giá trị zero tương ứng. Node này nằm trong tab Special và có thể được sử dụng ở mọi chế độ shader.

Khả năng của node này gần như vô hạn – bạn có thể viết các thủ tục phức tạp và tận dụng toàn bộ sức mạnh của shader dạng văn bản, chẳng hạn như vòng lặp, từ khóa ``discard``, các kiểu mở rộng, v.v. Ví dụ:

.. image:: img/vs_expression2.png

Nút Reroute
~~~~~~~~~~~

Node ``Reroute`` chỉ được sử dụng cho mục đích sắp xếp. Trong một shader phức tạp có nhiều node, bạn có thể thấy các đường nối giữa các node khiến mọi thứ khó đọc. Reroute, đúng như tên gọi, cho phép bạn điều chỉnh đường nối giữa các node để dễ đọc hơn. Bạn thậm chí có thể có nhiều node reroute trên cùng một đường nối, giúp tạo ra các góc vuông.

.. image:: img/vs_reroute.webp

Để di chuyển node reroute, hãy di chuyển con trỏ chuột lên trên node đó rồi nắm vào tay cầm xuất hiện.

.. image:: img/vs_reroute_handle.webp

Nút Fresnel
~~~~~~~~~~~

Node ``Fresnel`` được thiết kế để nhận các vector normal và view, đồng thời tạo ra một scalar là tích vô hướng đã bão hòa giữa chúng. Ngoài ra, bạn có thể thiết lập phép đảo và số mũ của phương trình. Node ``Fresnel`` rất phù hợp để thêm hiệu ứng chiếu sáng giống như viền cho các đối tượng.

.. image:: img/vs_fresnel.webp

Nút Boolean
~~~~~~~~~~~

Node ``Boolean`` có thể được chuyển đổi thành ``Scalar`` hoặc ``Vector`` để biểu diễn ``0`` hoặc ``1`` và ``(0, 0, 0)`` hoặc ``(1, 1, 1)`` tương ứng. Bạn có thể sử dụng thuộc tính này để bật hoặc tắt một số phần của hiệu ứng chỉ bằng một lần nhấp.

.. image:: img/vs_boolean.gif

Nút If
~~~~~~

Node ``If`` cho phép bạn thiết lập một vector sẽ được trả về dựa trên kết quả so sánh giữa ``a`` và ``b``. Có thể trả về ba vector: ``a == b`` (trong trường hợp đó, tham số tolerance được cung cấp làm ngưỡng so sánh – theo mặc định, nó bằng giá trị tối thiểu, tức là ``0.00001``), ``a > b`` và ``a < b``.

.. image:: img/vs_if.png

Nút Switch
~~~~~~~~~~

Node ``Switch`` trả về một vector nếu điều kiện boolean là ``true`` hoặc ``false``. ``Boolean`` đã được giới thiệu ở trên. Nếu muốn chuyển đổi một vector thành boolean true, tất cả các thành phần của vector phải khác zero.

.. image:: img/vs_switch.webp

Mesh Emitter
~~~~~~~~~~~~

Node ``Mesh Emitter`` được sử dụng để phát các particle từ các vertex của mesh. Tính năng này chỉ khả dụng cho các shader ở chế độ ``Particles``.

Hãy nhớ rằng không phải mọi đối tượng 3D đều là tệp mesh. Không thể kéo và thả tệp glTF vào graph. Tuy nhiên, bạn có thể tạo một scene kế thừa từ tệp đó, lưu mesh trong scene đó thành một tệp riêng rồi sử dụng tệp đó.

.. image:: img/vs_meshemitter.webp

Bạn cũng có thể kéo và thả các tệp obj vào graph editor để thêm node cho mesh cụ thể đó; các tệp mesh khác sẽ không hoạt động theo cách này.
