:article_outdated: True

.. _doc_animating_thousands_of_fish:

Tạo hiệu ứng chuyển động cho hàng nghìn con cá bằng MultiMeshInstance3D
=======================================================================

Tutorial này tìm hiểu một kỹ thuật được sử dụng trong game `ABZU <https://www.gdcvault.com/play/1024409/Creating-the-Art-of-ABZ>`_ để render và tạo hiệu ứng chuyển động cho hàng nghìn con cá bằng vertex animation và static mesh instancing.

Trong Godot, bạn có thể thực hiện việc này bằng một :ref:`Shader <class_Shader>` tùy chỉnh và một :ref:`MultiMeshInstance3D <class_MultiMeshInstance3D>`. Với kỹ thuật sau đây, bạn có thể render hàng nghìn object có chuyển động, ngay cả trên phần cứng cấu hình thấp.

Chúng ta sẽ bắt đầu bằng việc tạo chuyển động cho một con cá. Sau đó, chúng ta sẽ xem cách mở rộng chuyển động đó cho hàng nghìn con cá.

Tạo chuyển động cho một con cá
------------------------------

Chúng ta sẽ bắt đầu với một con cá duy nhất. Load model cá của bạn vào một :ref:`MeshInstance3D <class_MeshInstance3D>` và thêm một :ref:`ShaderMaterial <class_ShaderMaterial>` mới.

Đây là con cá chúng ta sẽ sử dụng trong các hình ảnh ví dụ; bạn có thể sử dụng bất kỳ model cá nào mình muốn.

.. image:: img/fish.png

.. note:: The fish model in this tutorial is made by `QuaterniusDev <https://quaternius.com>`_ and is
          được chia sẻ theo giấy phép creative commons. CC0 1.0 Universal (CC0 1.0) Public Domain Dedication https://creativecommons.org/publicdomain/zero/1.0/

Thông thường, bạn sẽ sử dụng bones và một :ref:`Skeleton3D <class_Skeleton3D>` để tạo chuyển động cho object. Tuy nhiên, bones được animate trên CPU, nên cuối cùng bạn phải tính toán hàng nghìn phép toán trong mỗi frame và việc có hàng nghìn object trở nên bất khả thi. Bằng cách sử dụng vertex animation trong vertex shader, bạn tránh phải dùng bones và thay vào đó có thể tính toán toàn bộ chuyển động chỉ bằng vài dòng code và hoàn toàn trên GPU.

Chuyển động sẽ gồm bốn chuyển động chính:

  1. 1. Chuyển động từ bên này sang bên kia 2. Chuyển động pivot quanh tâm của con cá 3. Chuyển động dạng sóng panning 4. Chuyển động xoắn panning

Toàn bộ code cho chuyển động sẽ nằm trong vertex shader, với các uniform điều khiển mức độ chuyển động. Chúng ta sử dụng uniform để điều khiển cường độ chuyển động, nhờ đó bạn có thể tinh chỉnh animation trong editor và xem kết quả theo thời gian thực mà không cần shader recompile.

Tất cả chuyển động sẽ được tạo bằng các cosine wave áp dụng cho ``VERTEX`` trong model space. Chúng ta muốn các vertex nằm trong model space để chuyển động luôn tương đối với hướng của con cá. Ví dụ, chuyển động từ bên này sang bên kia sẽ luôn di chuyển con cá tới lui theo hướng từ trái sang phải của nó, thay vì theo trục ``x`` trong hướng của world.

Để điều khiển tốc độ của animation, trước tiên chúng ta sẽ định nghĩa biến thời gian riêng bằng ``TIME``.

.. code-block:: glsl

  //time_scale là một uniform float
  float time = TIME * time_scale;

Chuyển động đầu tiên chúng ta sẽ triển khai là chuyển động từ bên này sang bên kia. Có thể tạo chuyển động này bằng cách offset ``VERTEX.x`` theo ``cos`` của ``TIME``. Mỗi khi mesh được render, tất cả vertex sẽ di chuyển sang bên một khoảng bằng ``cos(time)``.

.. code-block:: glsl

  //side_to_side là một uniform float
  VERTEX.x += cos(time) * side_to_side;

Animation tạo ra sẽ trông gần giống như sau:

.. image:: img/sidetoside.gif

Tiếp theo, chúng ta thêm pivot. Vì con cá nằm ở tâm (0, 0), tất cả những gì cần làm là nhân ``VERTEX`` với một rotation matrix để nó xoay quanh tâm của con cá.

Chúng ta tạo một rotation matrix như sau:

.. code-block:: glsl

  //angle được nhân với 0.1 để con cá chỉ pivot thay vì xoay hết một vòng
  //pivot là một uniform float
  float pivot_angle = cos(time) * 0.1 * pivot;
  mat2 rotation_matrix = mat2(vec2(cos(pivot_angle), -sin(pivot_angle)), vec2(sin(pivot_angle), cos(pivot_angle)));

Sau đó, chúng ta áp dụng nó trên các trục ``x`` và ``z`` bằng cách nhân nó với ``VERTEX.xz``.

.. code-block:: glsl

  VERTEX.xz = rotation_matrix * VERTEX.xz;

Chỉ với pivot được áp dụng, bạn sẽ thấy kết quả gần giống như sau:

.. image:: img/pivot.gif

Hai chuyển động tiếp theo cần chạy dọc theo xương sống của con cá. Để làm vậy, chúng ta cần một biến mới, ``body``. ``body`` là một float có giá trị ``0`` ở đuôi cá và ``1`` ở đầu cá.

.. code-block:: glsl

  float body = (VERTEX.z + 1.0) / 2.0; //đối với một con cá nằm ở tâm (0, 0) và có chiều dài bằng 2

Chuyển động tiếp theo là một cosine wave di chuyển dọc theo chiều dài của con cá. Để nó di chuyển theo xương sống của con cá, chúng ta offset input của ``cos`` theo vị trí dọc xương sống, tức biến ``body`` đã định nghĩa ở trên.

.. code-block:: glsl

  //wave là một uniform float
  VERTEX.x += cos(time + body) * wave;

Điều này rất giống với chuyển động từ bên này sang bên kia mà chúng ta đã định nghĩa ở trên, nhưng trong trường hợp này, bằng cách sử dụng ``body`` để offset ``cos``, mỗi vertex dọc theo xương sống sẽ có một vị trí khác nhau trong wave, khiến nó trông như một làn sóng đang di chuyển dọc theo con cá.

.. image:: img/wave.gif

Chuyển động cuối cùng là twist, tức một chuyển động roll panning dọc theo xương sống. Tương tự như pivot, trước tiên chúng ta tạo một rotation matrix.

.. code-block:: glsl

  //twist là một uniform float
  float twist_angle = cos(time + body) * 0.3 * twist;
  mat2 twist_matrix = mat2(vec2(cos(twist_angle), -sin(twist_angle)), vec2(sin(twist_angle), cos(twist_angle)));

Chúng ta áp dụng rotation trên các trục ``xy`` để con cá trông như đang roll quanh xương sống của nó. Để hoạt động đúng, xương sống của con cá cần nằm ở tâm của trục ``z``.

.. code-block:: glsl

  VERTEX.xy = twist_matrix * VERTEX.xy;

Đây là con cá sau khi áp dụng twist:

.. image:: img/twist.gif

Nếu áp dụng lần lượt tất cả các chuyển động này, chúng ta sẽ có một chuyển động mượt mà giống như thạch.

.. image:: img/all_motions.gif

Cá bình thường chủ yếu bơi bằng nửa thân phía sau. Vì vậy, chúng ta cần giới hạn các chuyển động panning ở nửa sau của con cá. Để làm vậy, chúng ta tạo một biến mới, ``mask``.

``mask`` là một float đi từ ``0`` ở phía trước con cá đến ``1`` ở phía cuối, sử dụng ``smoothstep`` để điều khiển điểm chuyển tiếp từ ``0`` sang ``1``.

.. code-block:: glsl

  //mask_black và mask_white là các uniform
  float mask = smoothstep(mask_black, mask_white, 1.0 - body);

Dưới đây là hình ảnh con cá với ``mask`` được sử dụng làm ``COLOR``:

.. image:: img/mask.png

Đối với wave, chúng ta nhân chuyển động với ``mask``, qua đó giới hạn nó ở nửa sau.

.. code-block:: glsl

  //chuyển động wave với mask
  VERTEX.x += cos(time + body) * mask * wave;

Để áp dụng mask cho twist, chúng ta sử dụng ``mix``. ``mix`` cho phép chúng ta trộn vị trí vertex giữa một vertex được xoay hoàn toàn và một vertex không được xoay. Chúng ta cần sử dụng ``mix`` thay vì nhân ``mask`` với ``VERTEX`` đã được xoay, vì chúng ta không cộng chuyển động vào ``VERTEX`` mà thay thế ``VERTEX`` bằng phiên bản đã xoay. Nếu nhân nó với ``mask``, chúng ta sẽ làm con cá bị thu nhỏ.

.. code-block:: glsl

  //chuyển động twist với mask
  VERTEX.xy = mix(VERTEX.xy, twist_matrix * VERTEX.xy, mask);

Kết hợp bốn chuyển động lại sẽ cho chúng ta animation cuối cùng.

.. image:: img/all_motions_mask.gif

Hãy thử điều chỉnh các uniform để thay đổi chu kỳ bơi của con cá. Bạn sẽ thấy mình có thể tạo ra rất nhiều kiểu bơi khác nhau bằng bốn chuyển động này.

Tạo một đàn cá
--------------

Godot giúp việc render hàng nghìn object giống nhau bằng node MultiMeshInstance3D trở nên dễ dàng.

Một node MultiMeshInstance3D được tạo và sử dụng giống như khi bạn tạo node MeshInstance3D. Trong tutorial này, chúng ta sẽ đặt tên node MultiMeshInstance3D là ``School``, vì nó sẽ chứa một đàn cá.

Sau khi có một MultiMeshInstance3D, hãy thêm một :ref:`MultiMesh <class_MultiMesh>`, rồi thêm :ref:`Mesh <class_Mesh>` của bạn với shader ở trên vào MultiMesh đó.

MultiMesh vẽ Mesh của bạn với ba thuộc tính bổ sung cho mỗi instance: Transform (rotation, translation, scale), Color và Custom. Custom được sử dụng để truyền vào 4 biến có thể tái sử dụng bằng một :ref:`Color <class_Color>`.

``instance_count`` chỉ định số instance của mesh mà bạn muốn vẽ. Hiện tại, hãy để ``instance_count`` ở ``0``, vì bạn không thể thay đổi bất kỳ tham số nào khác trong khi ``instance_count`` lớn hơn ``0``. Sau này chúng ta sẽ đặt ``instance count`` trong GDScript.

``transform_format`` chỉ định các transform được sử dụng là 3D hay 2D. Trong tutorial này, hãy chọn 3D.

Đối với cả ``color_format`` và ``custom_data_format``, bạn có thể chọn giữa ``None``, ``Byte`` và ``Float``. ``None`` có nghĩa là bạn sẽ không truyền dữ liệu đó (một biến ``COLOR`` cho mỗi instance hoặc ``INSTANCE_CUSTOM``) vào shader. ``Byte`` có nghĩa là mỗi số tạo nên màu bạn truyền vào sẽ được lưu bằng 8 bit, còn ``Float`` có nghĩa là mỗi số sẽ được lưu trong một số dấu phẩy động (32 bit). ``Float`` chậm hơn nhưng chính xác hơn, còn ``Byte`` sẽ tốn ít bộ nhớ hơn và nhanh hơn, nhưng có thể xuất hiện một số artifact hình ảnh.

Bây giờ, đặt ``instance_count`` thành số lượng cá mà bạn muốn có.

Tiếp theo, chúng ta cần thiết lập các transform cho mỗi instance.

Có hai cách để thiết lập transform cho mỗi instance của MultiMesh. Cách đầu tiên hoàn toàn thực hiện trong editor và được mô tả trong :ref:`MultiMeshInstance3D tutorial <doc_using_multi_mesh_instance>`.

Cách thứ hai là lặp qua tất cả instance và thiết lập transform của chúng trong code. Bên dưới, chúng ta sử dụng GDScript để lặp qua tất cả instance và đặt transform của chúng vào các vị trí ngẫu nhiên.

::

  for i in range($School.multimesh.instance_count):
    var position = Transform3D()
    position = position.translated(Vector3(randf() * 100 - 50, randf() * 50 - 25, randf() * 50 - 25))
    $School.multimesh.set_instance_transform(i, position)

Chạy script này sẽ đặt các con cá vào những vị trí ngẫu nhiên trong một hình hộp xung quanh vị trí của MultiMeshInstance3D.

.. note:: If performance is an issue for you, try running the scene with fewer fish.

Hãy chú ý rằng tất cả cá đều ở cùng một vị trí trong chu kỳ bơi. Điều này khiến chúng trông rất máy móc. Bước tiếp theo là tạo cho mỗi con cá một vị trí khác nhau trong chu kỳ bơi để toàn bộ đàn trông tự nhiên hơn.

Tạo chuyển động cho một đàn cá
------------------------------

Một trong những lợi ích của việc tạo chuyển động cho cá bằng các hàm ``cos`` là chúng được animate bằng một tham số, ``time``. Để tạo cho mỗi con cá một vị trí riêng trong chu kỳ bơi, chúng ta chỉ cần offset ``time``.

Chúng ta thực hiện việc đó bằng cách thêm giá trị custom cho mỗi instance ``INSTANCE_CUSTOM`` vào ``time``.

.. code-block:: glsl

  float time = (TIME * time_scale) + (6.28318 * INSTANCE_CUSTOM.x);

Tiếp theo, chúng ta cần truyền một giá trị vào ``INSTANCE_CUSTOM``. Chúng ta thực hiện việc đó bằng cách thêm một dòng vào vòng lặp ``for`` ở trên. Trong vòng lặp ``for``, chúng ta gán cho mỗi instance một tập gồm bốn float ngẫu nhiên để sử dụng.

::

  $School.multimesh.set_instance_custom_data(i, Color(randf(), randf(), randf(), randf()))

Giờ đây, tất cả cá đều có vị trí riêng trong chu kỳ bơi. Bạn có thể tạo thêm một chút khác biệt cho chúng bằng cách sử dụng ``INSTANCE_CUSTOM`` để khiến chúng bơi nhanh hơn hoặc chậm hơn bằng cách nhân với ``TIME``.

.. code-block:: glsl

  //đặt tốc độ từ 50% - 150% tốc độ thông thường
  float time = (TIME * (0.5 + INSTANCE_CUSTOM.y) * time_scale) + (6.28318 * INSTANCE_CUSTOM.x);

Bạn thậm chí có thể thử nghiệm việc thay đổi màu theo từng instance giống như cách bạn đã thay đổi giá trị tùy chỉnh theo từng instance.

Một vấn đề bạn sẽ gặp phải ở bước này là cá đã được animate nhưng chưa di chuyển. Bạn có thể khiến chúng di chuyển bằng cách cập nhật transform theo từng instance cho mỗi con cá trong từng frame. Mặc dù cách này sẽ nhanh hơn việc di chuyển hàng nghìn MeshInstance3Ds trong mỗi frame, nhưng nhiều khả năng nó vẫn sẽ chậm.

Trong tutorial tiếp theo, chúng ta sẽ tìm hiểu cách sử dụng :ref:`GPUParticles3D <class_GPUParticles3D>` để tận dụng GPU và di chuyển từng con cá một cách riêng lẻ, đồng thời vẫn nhận được lợi ích của instancing.
