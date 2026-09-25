:article_outdated: Đúng

.. _doc_animating_thousands_of_fish:

Tạo chuyển động cho hàng nghìn con cá bằng MultiMeshInstance3D
==============================================================

Tutorial này tìm hiểu một kỹ thuật được sử dụng trong trò chơi `ABZU <https://www.gdcvault.com/play/1024409/Creating-the-Art-of-ABZ>`_ để kết xuất và tạo chuyển động cho hàng nghìn con cá bằng vertex animation và static mesh instancing.

Trong Godot, bạn có thể thực hiện việc này bằng một :ref:`Shader <class_Shader>` tùy chỉnh và một :ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>`. Với kỹ thuật sau, bạn có thể kết xuất hàng nghìn đối tượng có chuyển động, ngay cả trên phần cứng cấp thấp.

Chúng ta sẽ bắt đầu bằng cách tạo chuyển động cho một con cá. Sau đó, chúng ta sẽ xem cách mở rộng chuyển động đó cho hàng nghìn con cá.

Tạo chuyển động cho một con cá
------------------------------

Chúng ta sẽ bắt đầu với một con cá duy nhất. Tải model cá vào :ref:`MeshInstance3D <class_MeshInstance3D>` rồi thêm một :ref:`ShaderMaterial <class_ShaderMaterial>` mới.

Đây là con cá chúng ta sẽ sử dụng trong các hình ảnh minh họa; bạn có thể dùng bất kỳ model cá nào mình muốn.

.. image:: img/fish.png

.. note:: Model cá trong tutorial này do `QuaterniusDev <https://quaternius.com>`_ tạo ra và được chia sẻ theo giấy phép creative commons. CC0 1.0 Universal (CC0 1.0) Public Domain Dedication https://creativecommons.org/publicdomain/zero/1.0/

Thông thường, bạn sẽ sử dụng bones và một :ref:`Skeleton3D <class_Skeleton3D>` để tạo chuyển động cho các đối tượng. Tuy nhiên, bones được tạo chuyển động trên CPU, vì vậy bạn sẽ phải tính toán hàng nghìn phép toán trong mỗi frame và việc có hàng nghìn đối tượng trở nên bất khả thi. Bằng cách sử dụng vertex animation trong vertex shader, bạn không cần dùng bones mà có thể tính toán toàn bộ chuyển động chỉ trong vài dòng code và hoàn toàn trên GPU.

Chuyển động sẽ gồm bốn chuyển động chính:

  1. Chuyển động từ bên này sang bên kia
  2. Chuyển động xoay quanh tâm của con cá
  3. Chuyển động dạng sóng quét dọc
  4. Chuyển động xoắn quét dọc

Toàn bộ code cho chuyển động sẽ nằm trong vertex shader, với các uniform điều khiển mức độ chuyển động. Chúng ta sử dụng uniform để điều khiển độ mạnh của chuyển động, nhờ đó bạn có thể tinh chỉnh chuyển động trong editor và xem kết quả theo thời gian thực mà không cần shader biên dịch lại.

Tất cả chuyển động sẽ được tạo bằng các sóng cosine áp dụng cho ``VERTEX`` trong model space. Chúng ta muốn các vertex ở trong model space để chuyển động luôn tương đối với hướng của con cá. Ví dụ, chuyển động từ bên này sang bên kia sẽ luôn di chuyển con cá qua lại theo hướng từ trái sang phải của nó, thay vì theo trục ``x`` trong hướng của world.

Để điều khiển tốc độ của chuyển động, trước tiên chúng ta sẽ định nghĩa biến thời gian riêng bằng ``TIME``.

.. code-block:: glsl

  //time_scale là một uniform float
  float time = TIME * time_scale;

Chuyển động đầu tiên chúng ta sẽ triển khai là chuyển động từ bên này sang bên kia. Có thể tạo chuyển động này bằng cách offset ``VERTEX.x`` theo ``cos`` của ``TIME``. Mỗi khi mesh được kết xuất, tất cả vertex sẽ di chuyển sang một bên theo giá trị ``cos(time)``.

.. code-block:: glsl

  //side_to_side là một uniform float
  VERTEX.x += cos(time) * side_to_side;

Chuyển động tạo ra sẽ trông như sau:

.. image:: img/sidetoside.gif

Tiếp theo, chúng ta thêm chuyển động xoay. Vì con cá được đặt tâm tại (0, 0), tất cả những gì cần làm là nhân ``VERTEX`` với một ma trận xoay để nó xoay quanh tâm của con cá.

Chúng ta dựng một ma trận xoay như sau:

.. code-block:: glsl

  //angle được scale theo 0.1 để con cá chỉ xoay một góc nhỏ thay vì xoay hết một vòng
  //pivot là một uniform float
  float pivot_angle = cos(time) * 0.1 * pivot;
  mat2 rotation_matrix = mat2(vec2(cos(pivot_angle), -sin(pivot_angle)), vec2(sin(pivot_angle), cos(pivot_angle)));

Sau đó, chúng ta áp dụng nó trên các trục ``x`` và ``z`` bằng cách nhân nó với ``VERTEX.xz``.

.. code-block:: glsl

  VERTEX.xz = rotation_matrix * VERTEX.xz;

Chỉ áp dụng chuyển động xoay, bạn sẽ thấy kết quả tương tự như sau:

.. image:: img/pivot.gif

Hai chuyển động tiếp theo cần quét dọc theo xương sống của con cá. Để làm vậy, chúng ta cần một biến mới là ``body``. ``body`` là một float có giá trị ``0`` ở đuôi cá và ``1`` ở đầu cá.

.. code-block:: glsl

  float body = (VERTEX.z + 1.0) / 2.0; //đối với một con cá đặt tâm tại (0, 0) và có chiều dài 2

Chuyển động tiếp theo là một sóng cosine di chuyển dọc theo chiều dài của con cá. Để nó di chuyển theo xương sống của cá, chúng ta offset đầu vào của ``cos`` theo vị trí trên xương sống, chính là biến ``body`` đã định nghĩa ở trên.

.. code-block:: glsl

  //wave là một uniform float
  VERTEX.x += cos(time + body) * wave;

Chuyển động này trông rất giống chuyển động từ bên này sang bên kia đã định nghĩa ở trên, nhưng ở đây, bằng cách sử dụng ``body`` để offset ``cos``, mỗi vertex dọc theo xương sống sẽ có một vị trí khác nhau trong sóng, khiến nó trông như một con sóng đang di chuyển dọc theo con cá.

.. image:: img/wave.gif

Chuyển động cuối cùng là xoắn, tức là một chuyển động lăn quét dọc theo xương sống. Tương tự như chuyển động xoay, trước tiên chúng ta dựng một ma trận xoay.

.. code-block:: glsl

  //twist là một uniform float
  float twist_angle = cos(time + body) * 0.3 * twist;
  mat2 twist_matrix = mat2(vec2(cos(twist_angle), -sin(twist_angle)), vec2(sin(twist_angle), cos(twist_angle)));

Chúng ta áp dụng phép xoay trên các trục ``xy`` để con cá trông như đang lăn quanh xương sống của nó. Để việc này hoạt động, xương sống của cá cần được đặt giữa trục ``z``.

.. code-block:: glsl

  VERTEX.xy = twist_matrix * VERTEX.xy;

Đây là con cá sau khi áp dụng chuyển động xoắn:

.. image:: img/twist.gif

Nếu áp dụng lần lượt tất cả các chuyển động này, chúng ta sẽ có một chuyển động mềm mại giống như thạch.

.. image:: img/all_motions.gif

Cá thật chủ yếu bơi bằng nửa thân phía sau. Vì vậy, chúng ta cần giới hạn các chuyển động quét ở nửa sau của con cá. Để làm vậy, chúng ta tạo một biến mới là ``mask``.

``mask`` là một float đi từ ``0`` ở phía trước con cá đến ``1`` ở phía sau, sử dụng ``smoothstep`` để điều khiển điểm mà quá trình chuyển tiếp từ ``0`` sang ``1`` diễn ra.

.. code-block:: glsl

  //mask_black và mask_white là các uniform
  float mask = smoothstep(mask_black, mask_white, 1.0 - body);

Dưới đây là hình ảnh con cá với ``mask`` được sử dụng làm ``COLOR``:

.. image:: img/mask.png

Đối với sóng, chúng ta nhân chuyển động với ``mask``, qua đó giới hạn nó ở nửa sau.

.. code-block:: glsl

  //chuyển động dạng sóng với mask
  VERTEX.x += cos(time + body) * mask * wave;

Để áp dụng mask cho chuyển động xoắn, chúng ta sử dụng ``mix``. ``mix`` cho phép chúng ta trộn vị trí vertex giữa một vertex được xoay hoàn toàn và một vertex không bị xoay. Chúng ta cần sử dụng ``mix`` thay vì nhân ``mask`` với ``VERTEX`` đã xoay, vì chúng ta không cộng chuyển động vào ``VERTEX`` mà đang thay thế ``VERTEX`` bằng phiên bản đã xoay. Nếu nhân giá trị đó với ``mask``, chúng ta sẽ làm con cá bị co lại.

.. code-block:: glsl

  //chuyển động xoắn với mask
  VERTEX.xy = mix(VERTEX.xy, twist_matrix * VERTEX.xy, mask);

Kết hợp bốn chuyển động lại với nhau, chúng ta có chuyển động hoàn chỉnh.

.. image:: img/all_motions_mask.gif

Hãy thử thay đổi các uniform để điều chỉnh chu kỳ bơi của cá. Bạn sẽ thấy rằng mình có thể tạo ra rất nhiều kiểu bơi khác nhau bằng bốn chuyển động này.

Tạo một đàn cá
--------------

Godot giúp bạn dễ dàng hiển thị hàng nghìn đối tượng giống nhau bằng node MultiMeshInstance3D.

Bạn tạo và sử dụng node MultiMeshInstance3D theo cách giống như khi tạo node MeshInstance3D. Trong tutorial này, chúng ta sẽ đặt tên cho node MultiMeshInstance3D là ``School``, vì node này sẽ chứa một đàn cá.

Sau khi có một MultiMeshInstance3D, hãy thêm một :ref:`MultiMesh <class_MultiMesh>`, rồi thêm :ref:`Mesh <class_Mesh>` cùng shader ở trên vào MultiMesh đó.

MultiMesh vẽ Mesh của bạn với ba thuộc tính bổ sung cho mỗi instance: Transform (xoay, dịch chuyển, tỉ lệ), Color và Custom. Custom được dùng để truyền vào 4 biến đa dụng thông qua một :ref:`Color <class_Color>`.

``instance_count`` xác định số instance của mesh mà bạn muốn vẽ. Hiện tại, hãy để ``instance_count`` ở ``0`` vì bạn không thể thay đổi các tham số khác khi ``instance_count`` lớn hơn ``0``. Sau này chúng ta sẽ thiết lập ``instance count`` trong GDScript.

``transform_format`` xác định các transform được sử dụng là 3D hay 2D. Trong tutorial này, hãy chọn 3D.

Đối với cả ``color_format`` và ``custom_data_format``, bạn có thể chọn giữa ``None``, ``Byte`` và ``Float``. ``None`` nghĩa là bạn sẽ không truyền dữ liệu đó (một biến ``COLOR`` cho mỗi instance hoặc ``INSTANCE_CUSTOM``) vào shader. ``Byte`` nghĩa là mỗi số tạo nên màu bạn truyền vào sẽ được lưu bằng 8 bit, còn ``Float`` nghĩa là mỗi số sẽ được lưu dưới dạng số dấu phẩy động (32 bit). ``Float`` chậm hơn nhưng chính xác hơn, còn ``Byte`` tốn ít bộ nhớ hơn và nhanh hơn, nhưng bạn có thể thấy một số lỗi hiển thị.

Bây giờ, hãy đặt ``instance_count`` thành số lượng cá bạn muốn có.

Tiếp theo, chúng ta cần thiết lập các transform cho mỗi instance.

Có hai cách để thiết lập transform cho mỗi instance của MultiMesh. Cách đầu tiên hoàn toàn thực hiện trong editor và được mô tả trong tutorial :ref:`MultiMeshInstance3D tutorial <doc_using_multi_mesh_instance>`.

Cách thứ hai là lặp qua tất cả instance và thiết lập transform của chúng trong code. Bên dưới, chúng ta dùng GDScript để lặp qua tất cả instance và đặt transform của chúng vào các vị trí ngẫu nhiên.

::

  for i in range($School.multimesh.instance_count):
    var position = Transform3D()
    position = position.translated(Vector3(randf() * 100 - 50, randf() * 50 - 25, randf() * 50 - 25))
    $School.multimesh.set_instance_transform(i, position)

Chạy script này sẽ đặt cá vào các vị trí ngẫu nhiên trong một hình hộp xung quanh vị trí của MultiMeshInstance3D.

.. note:: Nếu hiệu năng là vấn đề đối với bạn, hãy thử chạy scene với ít cá hơn.

Hãy chú ý rằng tất cả cá đều đang ở cùng một vị trí trong chu kỳ bơi? Điều này khiến chúng trông rất máy móc. Bước tiếp theo là đặt mỗi con cá ở một vị trí khác nhau trong chu kỳ bơi để toàn bộ đàn cá trông tự nhiên hơn.

Tạo hoạt ảnh cho một đàn cá
---------------------------

Một trong những lợi ích của việc tạo hoạt ảnh cho cá bằng các hàm ``cos`` là chúng được tạo hoạt ảnh với một tham số, ``time``. Để tạo cho mỗi con cá một vị trí riêng trong chu kỳ bơi, chúng ta chỉ cần thêm độ lệch vào ``time``.

Chúng ta thực hiện việc đó bằng cách cộng giá trị custom cho mỗi instance ``INSTANCE_CUSTOM`` vào ``time``.

.. code-block:: glsl

  float time = (TIME * time_scale) + (6.28318 * INSTANCE_CUSTOM.x);

Tiếp theo, chúng ta cần truyền một giá trị vào ``INSTANCE_CUSTOM``. Chúng ta thực hiện việc đó bằng cách thêm một dòng vào vòng lặp ``for`` ở trên. Trong vòng lặp ``for``, chúng ta gán cho mỗi instance một tập gồm bốn số thực ngẫu nhiên để sử dụng.

::

  $School.multimesh.set_instance_custom_data(i, Color(randf(), randf(), randf(), randf()))

Giờ đây, tất cả cá đều có vị trí riêng trong chu kỳ bơi. Bạn có thể khiến chúng khác biệt hơn một chút bằng cách sử dụng ``INSTANCE_CUSTOM`` để làm chúng bơi nhanh hơn hoặc chậm hơn bằng cách nhân với ``TIME``.

.. code-block:: glsl

  //đặt tốc độ từ 50% - 150% tốc độ thông thường
  float time = (TIME * (0.5 + INSTANCE_CUSTOM.y) * time_scale) + (6.28318 * INSTANCE_CUSTOM.x);

Bạn thậm chí có thể thử thay đổi màu cho mỗi instance theo cách tương tự như khi thay đổi giá trị custom cho mỗi instance.

Một vấn đề bạn sẽ gặp phải lúc này là cá đã được tạo hoạt ảnh nhưng không di chuyển. Bạn có thể di chuyển chúng bằng cách cập nhật transform cho mỗi instance của từng con cá trong mỗi frame. Mặc dù cách này sẽ nhanh hơn việc di chuyển hàng nghìn MeshInstance3D trong mỗi frame, nhưng nhiều khả năng nó vẫn chậm.

Trong tutorial tiếp theo, chúng ta sẽ tìm hiểu cách sử dụng :ref:`GPUParticles3D <class_GPUParticles3D>` để tận dụng GPU và di chuyển từng con cá riêng lẻ, đồng thời vẫn nhận được lợi ích của instancing.

.. _`ABZU`: https://www.gdcvault.com/play/1024409/Creating-the-Art-of-ABZ
.. _`QuaterniusDev`: https://quaternius.com
