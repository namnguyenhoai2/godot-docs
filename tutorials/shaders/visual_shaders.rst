.. _doc_visual_shaders:

Sử dụng VisualShaders
=====================

VisualShaders là một lựa chọn trực quan để tạo shader.

Vì shader vốn gắn liền với hình ảnh, cách tiếp cận dựa trên graph với bản xem trước của texture, material, v.v. mang lại nhiều tiện lợi hơn so với shader hoàn toàn dựa trên script. Mặt khác, VisualShaders không cung cấp tất cả tính năng của shader script, vì vậy có thể cần sử dụng song song cả hai để tạo các hiệu ứng cụ thể.

.. note::

    Nếu bạn chưa quen với shader, hãy bắt đầu bằng cách đọc
    :ref:`doc_introduction_to_shaders`.

Tạo một VisualShader
--------------------

VisualShader có thể được tạo trong bất kỳ :ref:`class_ShaderMaterial` nào. Để bắt đầu sử dụng VisualShader, hãy tạo một ``ShaderMaterial`` mới trong đối tượng tùy ý.

.. image:: img/shader_material_create_mesh.webp

Sau đó, gán một resource :ref:`class_Shader` cho thuộc tính ``Shader``.

.. image:: img/visual_shader_create.webp

Nhấp vào resource ``Shader`` mới và hộp thoại Create Shader sẽ tự động mở. Thay đổi tùy chọn Type thành :ref:`class_VisualShader` trong menu thả xuống, sau đó đặt tên cho shader.

.. image:: img/visual_shader_create2.webp

Nhấp vào visual shader vừa tạo để mở Shader Editor. Bố cục của Shader Editor gồm bốn phần: danh sách file ở bên trái, thanh công cụ phía trên, graph ở giữa và phần xem trước material ở bên phải, có thể tắt

.. image:: img/visual_shader_editor2.webp

Từ trái sang phải trong thanh công cụ:

- Mũi tên dùng để bật hoặc tắt khả năng hiển thị của bảng file. - Nút ``File`` mở menu thả xuống để lưu, tải và tạo file. - Nút ``Add Node`` hiển thị menu popup, cho phép bạn thêm node vào shader graph. - Menu thả xuống là loại shader: Vertex, Fragment và Light. Giống như với script shader, menu này xác định các node dựng sẵn nào sẽ khả dụng. - Các nút tiếp theo và ô nhập số điều khiển mức zoom, tính năng bắt dính theo grid và khoảng cách giữa các đường grid (tính bằng pixel). - Công tắc này điều khiển việc minimap của graph ở góc dưới bên phải của editor có hiển thị hay không. - Nút tự động sắp xếp các node đã chọn sẽ cố gắng tổ chức mọi node bạn chọn một cách hiệu quả và gọn gàng nhất có thể. - Nút Manage Varyings mở menu thả xuống cho phép bạn thêm hoặc xóa một varying. - Nút hiển thị code được tạo ra sẽ hiển thị shader code tương ứng với graph của bạn. - Công tắc này bật hoặc tắt phần xem trước material. - Nút ``Online Docs`` mở trang tài liệu này trong trình duyệt web. - Nút cuối cùng cho phép bạn đưa shader editor vào một cửa sổ riêng, tách khỏi phần còn lại của editor.

.. note::

    Mặc dù VisualShader không yêu cầu viết code, chúng vẫn dùng chung logic với script shader. Bạn nên học những kiến thức cơ bản của cả hai để hiểu rõ pipeline shading.

    Visual shader graph được chuyển đổi thành script shader ở phía sau, và bạn có thể xem code này bằng cách nhấn nút cuối cùng trên thanh công cụ. Điều này có thể giúp bạn hiểu một node nhất định thực hiện gì và cách tái tạo nó bằng script.

Sử dụng Visual Shader Editor
----------------------------

Theo mặc định, mọi ``VisualShader`` mới đều có một output node. Mỗi kết nối node kết thúc tại một trong các socket của output node. Node là đơn vị cơ bản để tạo shader. Để thêm node mới, hãy nhấp vào nút ``Add Node`` ở góc trên bên trái hoặc nhấp chuột phải vào bất kỳ vị trí trống nào trong graph; một menu sẽ bật lên.

.. image:: img/vs_popup.webp

Popup này có các đặc điểm sau:

- Nếu bạn nhấp chuột phải vào graph, menu này sẽ được gọi tại vị trí con trỏ và node được tạo trong trường hợp đó cũng sẽ được đặt bên dưới vị trí ấy; nếu không, node sẽ được tạo ở trung tâm graph. - Popup có thể được thay đổi kích thước theo chiều ngang và chiều dọc, cho phép hiển thị nhiều nội dung hơn. Biến đổi kích thước và vị trí nội dung của tree được lưu lại giữa các lần mở, vì vậy nếu bạn vô tình đóng popup, bạn có thể dễ dàng khôi phục trạng thái trước đó. - Các tùy chọn ``Expand All`` và ``Collapse All`` trong menu tùy chọn thả xuống có thể được dùng để dễ dàng liệt kê các node khả dụng. - Bạn cũng có thể kéo và thả node từ popup vào graph.

Mặc dù popup sắp xếp các node theo danh mục, ban đầu nó có thể khiến bạn thấy choáng ngợp. Hãy thử thêm một số node, kết nối chúng vào output socket và quan sát điều gì xảy ra.

Khi kết nối bất kỳ output ``scalar`` nào với input ``vector``, tất cả component của vector sẽ nhận giá trị của scalar.

Khi kết nối bất kỳ output ``vector`` nào với input ``scalar``, giá trị của scalar sẽ là giá trị trung bình của các component trong vector.

Giao diện node của Visual Shader
--------------------------------

Node của Visual Shader có các port input và output. Port input nằm ở phía bên trái của node, còn port output nằm ở phía bên phải của node.

.. figure:: img/vs_node.webp

Các port này được tô màu để phân biệt loại port:

.. |scalar| image:: img/vs_scalar.webp
.. |vector| image:: img/vs_vector.webp
.. |boolean| image:: img/vs_boolean.webp
.. |transform| image:: img/vs_transform.webp
.. |sampler| image:: img/vs_sampler.webp


.. list-table:: Port types
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
     - Xanh lá
     - Bật hoặc tắt, đúng hoặc sai.
     - |boolean|
   * - Transform
     - Hồng
     - Một ma trận, thường được dùng để biến đổi vertex.
     - |transform|
   * - Sampler
     - Cam
     - Một texture sampler. Có thể dùng nó để lấy mẫu texture.
     - |sampler|

Tất cả các loại này được sử dụng trong phép tính của vertex, fragment và light trong shader. Ví dụ: phép nhân ma trận, phép cộng vector hoặc phép chia scalar.

Có những loại khác, nhưng đây là các loại chính.

Các node của Visual Shader
--------------------------

Dưới đây là một số node đặc biệt mà bạn nên biết. Danh sách này không đầy đủ và có thể được mở rộng thêm với nhiều node và ví dụ khác.

Node Expression
~~~~~~~~~~~~~~~

Node ``Expression`` cho phép bạn viết các biểu thức Godot Shading Language (tương tự GLSL) bên trong visual shader. Node này có các nút để thêm số lượng tùy ý các port input và output cần thiết, đồng thời có thể thay đổi kích thước. Bạn cũng có thể thiết lập tên và loại của từng port. Biểu thức bạn nhập sẽ được áp dụng ngay cho material (sau khi focus rời khỏi ô nhập biểu thức). Mọi lỗi phân tích hoặc biên dịch sẽ được in ra tab Output. Theo mặc định, các output được khởi tạo với giá trị zero tương ứng. Node này nằm trong tab Special và có thể được sử dụng ở mọi chế độ shader.

Khả năng của node này gần như vô hạn – bạn có thể viết các thủ tục phức tạp và sử dụng toàn bộ sức mạnh của shader dựa trên text, chẳng hạn như vòng lặp, từ khóa ``discard``, các kiểu mở rộng, v.v. Ví dụ:

.. image:: img/vs_expression2.png

Node Reroute
~~~~~~~~~~~~

Node ``Reroute`` chỉ được dùng cho mục đích tổ chức. Trong một shader phức tạp với nhiều node, bạn có thể thấy các đường nối giữa các node khiến việc đọc trở nên khó khăn. Reroute, đúng như tên gọi, cho phép bạn điều chỉnh đường nối giữa các node để chúng dễ đọc hơn. Bạn thậm chí có thể có nhiều node reroute trên cùng một đường nối, dùng để tạo các góc vuông.

.. image:: img/vs_reroute.webp

Để di chuyển node reroute, hãy đưa con trỏ chuột lên nó rồi kéo tay nắm xuất hiện.

.. image:: img/vs_reroute_handle.webp

Node Fresnel
~~~~~~~~~~~~

Node ``Fresnel`` được thiết kế để nhận các vector normal và view, sau đó tạo ra một scalar là tích vô hướng đã bão hòa giữa chúng. Ngoài ra, bạn có thể thiết lập phép đảo và số mũ của phương trình. Node ``Fresnel`` rất hữu ích để thêm hiệu ứng ánh sáng giống như viền sáng cho các đối tượng.

.. image:: img/vs_fresnel.webp

Node Boolean
~~~~~~~~~~~~

Node ``Boolean`` có thể được chuyển đổi thành ``Scalar`` hoặc ``Vector`` để biểu diễn ``0`` hoặc ``1`` và ``(0, 0, 0)`` hoặc ``(1, 1, 1)`` tương ứng. Có thể dùng thuộc tính này để bật hoặc tắt một số phần của hiệu ứng chỉ bằng một lần nhấp.

.. image:: img/vs_boolean.gif

Node If
~~~~~~~

Node ``If`` cho phép bạn thiết lập một vector sẽ được trả về dựa trên kết quả so sánh giữa ``a`` và ``b``. Có ba vector có thể được trả về: ``a == b`` (trong trường hợp đó, tham số tolerance được cung cấp dưới dạng ngưỡng so sánh – theo mặc định, nó bằng giá trị nhỏ nhất, tức là ``0.00001``), ``a > b`` và ``a < b``.

.. image:: img/vs_if.png

Node Switch
~~~~~~~~~~~

Node ``Switch`` trả về một vector nếu điều kiện boolean là ``true`` hoặc ``false``. ``Boolean`` đã được giới thiệu ở trên. Nếu muốn chuyển đổi một vector thành boolean true, tất cả component của vector phải khác zero.

.. image:: img/vs_switch.webp

Mesh Emitter
~~~~~~~~~~~~

Node ``Mesh Emitter`` được dùng để phát particle từ các vertex của mesh. Node này chỉ khả dụng cho các shader ở chế độ ``Particles``.

Hãy nhớ rằng không phải mọi đối tượng 3D đều là file mesh. Không thể kéo và thả file glTF vào graph. Tuy nhiên, bạn có thể tạo một scene kế thừa từ file đó, lưu mesh trong scene ấy thành file riêng và sử dụng file đó.

.. image:: img/vs_meshemitter.webp

Bạn cũng có thể kéo và thả các file obj vào graph editor để thêm node cho mesh cụ thể đó; các file mesh khác sẽ không hoạt động theo cách này.
